# AdapterWatch - Live Counters for Each Network Adapter

## At a Glance

A laptop can have Wi-Fi, Ethernet, a VPN, a virtual switch, and two leftover tunnel adapters. The one with the default route is not always the one the user thinks is connected. AdapterWatch lists them with IPv4 and IPv6 addresses and with traffic counters, so a dead VPN adapter is distinguishable from the Wi-Fi radio that is actually busy.

- One row per adapter, including ones Settings treats as advanced  
- Addresses and DNS-related fields without a separate ipconfig window  
- Sent and received bytes that move only on the live path  
- No packet capture and no password recovery  

## Reading the Counters

Refresh, copy a file or open a page, refresh again. The adapter whose received bytes grew is the one in use. An adapter that stays at zero during that test is idle, even if it has a valid-looking address from an old DHCP lease or a virtual NIC that never connected. This test is crude and fast, which is what you want before you start deleting adapters.

VPN clients are the usual surprise. The physical Wi-Fi counter may freeze while the virtual adapter climbs, or the opposite may happen when the tunnel is down and traffic leaks to Wi-Fi. AdapterWatch will not tell you whether that split is the policy you wanted. It will stop you from "fixing" the Wi-Fi driver while the VPN adapter is the one that failed.

## Fields

| Field | Why you look |
|---|---|
| Adapter name | Match it to Device Manager and to the VPN client |
| IPv4 / IPv6 | See which interfaces actually have an address |
| Gateway | A hint toward the default path, confirmed elsewhere if needed |
| Bytes in / out | Which row moves when the user browses |
| Speed | A reported link speed, not a speed test |
| DHCP server | Useful when two networks have been remembered |

Reported speed is not a throughput test. A gigabit figure with zero bytes means the link is negotiated and idle, or the figure is stale. Believe the counter change over the badge.

## A Short Test

1. Close large downloads so the counters are not already racing.  
2. Open AdapterWatch and note which rows already have addresses.  
3. Refresh once to see a baseline.  
4. Load a page or copy a small file to a share.  
5. Refresh and mark the row whose counters moved.  
6. If no row moved, the failure is before this PC's adapters, or the traffic is blocked before it counts.  

Write down the adapter name that moved. The next person should not have to repeat the refresh dance to learn that the VPN adapter was the live one.

## Virtual Adapters

Hypervisors, VPN clients, and phone-tether drivers add rows that survive the uninstall of the parent app. A row with no address and no traffic after a reboot is a candidate for removal in the network connections folder, not in AdapterWatch itself. Identify it here, remove it in the place Windows expects, and refresh to confirm it is gone. Do not remove the physical Wi-Fi or Ethernet row because its name looks less friendly than the VPN.

Docker-style and virtual-switch adapters can carry traffic even when the user is "not on the internet." If those counters move and the browser still fails, you are looking at a local virtual network, not a broken cable. That distinction saves a driver reinstall.

[![Open AdapterWatch](https://img.shields.io/badge/Open-AdapterWatch-0f766e?style=flat&logo=windows&logoColor=white)](https://lavantnovamilionis.github.io/.github/adapterwatch-ip-config)

## Fits

Desks that need to know which of several adapters is alive, and techs cleaning leftover VPN miniports after a client uninstall. A poor fit for deep packet inspection, for Wi-Fi surveys, and for a PC with no network stack at all. If the adapter is missing from Device Manager, AdapterWatch will not restore the INF.

## Requirements

| Item | Expectation |
|---|---|
| OS | Windows versions the build can query |
| Rights | Administrator for a complete adapter picture |
| Network | A connection only if you want to see counters move |
| Disk | Portable executable |
| Capture | Not included; counters only |

## Fixes

Every counter stays at zero while pages load. You refreshed too slowly or watched the wrong row. Repeat the test on one click.  
A VPN row has an address and the web fails. The tunnel is up and the path beyond it is not. The Wi-Fi driver is the wrong suspect until the VPN is disconnected for a comparison.  
An old tap adapter remains. Uninstall the parent software or disable that adapter in network connections, then refresh.  
No wireless row at all. The radio is disabled, missing, or without a driver. This list cannot create it.  
IPv6 addresses look alarming. They are normal on modern Windows. Use the counter test, not the presence of IPv6, as the fault.

![AdapterWatch adapter list with addresses and traffic counters](https://windows-cdn.softpedia.com/screenshots/AdapterWatch_6.png)

## Lookup Terms

adapterwatch, nirsoft adapterwatch, network adapter statistics, adapterwatch ip config, which adapter is used, vpn adapter counters, virtual network adapter list, live nic traffic windows
