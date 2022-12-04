# About iptable module

`Iptables` and `ip6tables` are used to set up, maintain, and inspect the tables
of `IPv4` and `IPv6` packet filter rules in the Linux kernel.

Basically, it uses different `tables` to group different `chains` with a set
of `rules`:

`table --> chains --> rules`

</br>

### 1. Default tables and built-in chains

| Table | Built-in chains | Desc |
| ------ | --------------- | -------------|
| filter | | Default table (if no `-t` option provided), is responsible for filtering the incoming and outgoing packets on the current computer|
|       | INPUT | Packet to come in|
|       | OUTPUT | Packet to go out|
|       | FORWARD | Packet to pass through, usually only used when current computer configured as a `Router`|
| ------ | --------------- | -------------|
| nat | | Network address translation |
|       | PREROUTING | For altering packets as soon as they come in |
|       | OUTPUT | For altering outgoing packets before routing|
|       | POSTROUTING | For altering packets before they go out|
| ------ | --------------- | -------------|
| mangle | | Special use case|
|       | PREROUTING | For altering incoming packets before routing |
|       | OUTPUT | For altering outgoing packets before routing|
|       | INPUT | For packets coming into|
|       | POSTROUTING | For altering packets as they're about to go out|

</br>

### 2. How to flush tables (delete all chain's rules)

```bash
#=============================================================================
# Flush all tables and chains
#=============================================================================
iptables --table filter --flush
iptables --table filter --zero
iptables --table nat --flush
iptables --table nat --zero
iptables --table mangle --flush
iptables --table mangle --zero
```

`--flush` and `--zero` act on all chains in all tables if you don't provide
`-t/--table` option, so the following command has the same result with above
commands:

```bash
iptables --flush
iptables --zero
```

</br>

### 3. Terms and value meaning

Sample command:

`iptables -A {INPUT|OUTPUT} -p icmp --icmp-type {echo-reply|echo-request} -m state --state NEW,ESTABLISHED,RELATED -j {ACCEPT|REJECT|DROP}
`

</br>

- `-A/--append`: Append new rule to the chain

- `-p/--protocol`: Specific protocol, available protocol names are located in `/etc/protocols`

- `--icmp-type`: For more protocol match options, run `iptables -p PROTOCOL_NAME --help | bat`

- `-m/--match --state`: Specifies match to use:

    - `INVALID`:
        the packet could not be identified for some reason which includes running
        out of memory and ICMP errors which don't correspond to any known connection.

    - `NEW`:
        the packet has started a new connection, or otherwise associated with a
        connection which has not seen packets in both directions.

    - `ESTABLISHED`:
        the packet is associated with a connection which has seen packets in both
        directions.

    - `RELATED`:
        the packet is starting a new connection, but is associated with an existing
        connection, such as an FTP data transfer, or an ICMP error.

    - `UNTRACKED`:
        the packet is not tracked at all, which happens if you use the `NOTRACK`
        target in raw table.

- `-j/--jump` `target` value

    - `ACCEPT` means to let the packet through.

    - `DROP` means to drop the packet on the floor.

    - `RETURN` means stop traversing this chain  and  resume  at the  next rule
    in the previous (calling) chain.

    </br>



### 3. How to set tables policy

The default `action` (aka: `target`) if there are no rules to be matched:

```bash
#=============================================================================
# Default policies: DROP
#=============================================================================
iptables --policy INPUT DROP
iptables --policy FORWARD DROP
iptables --policy OUTPUT DROP

# iptables --table nat --policy PREROUTING  DROP
# iptables --table nat --policy INPUT DROP
# iptables --table nat --policy OUTPUT DROP
# iptables --table nat --policy POSTROUTING DROP
#
# iptables --table mangle --policy PREROUTING  DROP
# iptables --table mangle --policy INPUT DROP
# iptables --table mangle --policy OUTPUT DROP
# iptables --table mangle --policy POSTROUTING DROP
```

If you don't provide `-t/--table` option, by default `iptables` applies to the
`filter` table.

</br>

#### 4. Special rules

- If default policy is `DROP` for `INPUT & OUPUT` chains

    Then the following rules are saying:

    > Allow all outgoing for all protocols and ports

    > Allow all incoming on top of established connection

    ```bash
    iptables -t filter --append INPUT  --match state --state ESTABLISHED,RELATED     --jump ACCEPT
    iptables -t filter --append OUTPUT --match state --state NEW,ESTABLISHED,RELATED --jump ACCEPT
    ```

    It's very convenient and useful for reducing `OUTPUT` chain rules setup.

    </br>


- Allow all incoming packets via `lo` NIC

    ```bash
    #
    # Allow all incoming packets from `localhost`
    #
    iptables --append INPUT --in-interface $local_interface --jump ACCEPT
    ```

    </br>

- Multi dest port case

    When dealing with mulitple dest ports, you have to use:

    `--match multiport --dports PORT1,PORT2`

    Sample:

    ```bash
    iptables --append INPUT --protocol TCP --match multiport --dports 9099,8080 --jump ACCEPT
    ```

    </br>


