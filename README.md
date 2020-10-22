# Chrony NTP Client Ansible role

## Description
NTP Client (chrony) for Ansible, for all your high-precision timekeeping.

## Supported features
* Customizable NTP server pool;
* No ingress networking (NTP daemon doesn't try to bind to NTP port, so no external access is possible);
* Full real-time clock support;
* (Optional) Continuous RTC monitoring and setting, requires exclusive RTC access.

## Configuration
All variables of this role are namespaced under the `ntp_*` prefix.

Apple and Cloudflare's public NTP servers are quite good and deliver
high-precision NTP data fast, so they are included in the list.

### Available variables
| Option                  | Default value                                               | Description                                                                                                               |
|-------------------------|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| `pools`                 | `["pool.ntp.org", "time.apple.com", "time.cloudflare.com"]` | NTP server pools list.                                                                                                    |
| `hwclock_path`          | `/dev/rtc`                                                  | RTC device path.                                                                                                          |
| `force_utc`             | *false*                                                     | Force storing UTC time in hardware clock.                                                                                 |
| `force_hwclock_control` | *false*                                                     | (Not recommended) Force Chrony to take over RTC device for itself. Breaks all other utilities that may access RTC device. |
| `rtc_tracking_path`     | `/var/lib/chrony/rtc`                                       | Path for Chrony's RTC tracking files. Only used if `force_hwclock_control == true`.                                       |
| `realtime`              | *true*                                                      | (Recommended) Use real-time scheduling priority.                                                                          |
