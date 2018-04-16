LimitNOFILE=64000

sudo sysctl net.core.somaxconn=2048
sudo sysctl net.core.netdev_max_backlog=2000
sudo sysctl net.ipv4.tcp_max_syn_backlog=2048
sudo sysctl net.ipv4.tcp_fin_timeout=10
sudo sysctl net.ipv4.tcp_tw_recycle=1
sudo sysctl net.ipv4.tcp_tw_reuse=1


# /etc/sysctl.conf
fs.file-max = 196608
net.ipv4.ip_forward = 0
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_synack_retries = 2
net.ipv4.tcp_syn_retries = 2
net.core.netdev_max_backlog = 64000
net.ipv4.tcp_moderate_rcvbuf = 1
net.ipv4.tcp_orphan_retries = 2
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_max_orphans = 64000
net.ipv4.tcp_max_syn_backlog = 64000
net.ipv4.tcp_fin_timeout = 4
net.ipv4.netfilter.ip_conntrack_max = 196608
net.netfilter.nf_conntrack_tcp_timeout_established = 600
net.netfilter.nf_conntrack_max = 196608
net.netfilter.nf_conntrack_tcp_timeout_syn_sent = 15
# net.netfilter.nf_conntrack_checksum = 0
net.nf_conntrack_max = 196608
net.ipv4.tcp_keepalive_time = 60
net.ipv4.tcp_keepalive_intvl = 10
net.ipv4.tcp_keepalive_probes = 3
# net.ipv4.ip_local_port_range = 1025 65535
net.core.somaxconn = 64000
# net.ipv4.tcp_max_tw_buckets = 2000000
# net.ipv4.tcp_timestamps = 0




# cat /etc/sysctl.conf
net.ipv4.ip_forward = 0
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_synack_retries = 2
net.ipv4.tcp_syn_retries = 2
net.ipv4.conf.default.forwarding = 0
net.ipv4.conf.default.proxy_arp = 0
net.ipv4.conf.default.send_redirects = 1
net.ipv4.conf.all.rp_filter = 0
net.ipv4.conf.all.send_redirects = 0
kernel.sysrq = 1
net.ipv4.icmp_echo_ignore_broadcasts = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.icmp_ignore_bogus_error_responses = 1
net.core.rmem_max = 33554432
net.core.wmem_max = 33554432
net.ipv4.tcp_rmem = 4096 87380 33554432
net.ipv4.tcp_wmem = 4096 65536 33554432
net.core.netdev_max_backlog = 262144
net.ipv4.tcp_no_metrics_save = 1
net.ipv4.tcp_moderate_rcvbuf = 1
net.ipv4.tcp_orphan_retries = 2
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_max_orphans = 262144
net.ipv4.tcp_max_syn_backlog = 262144
net.ipv4.tcp_fin_timeout = 4
vm.min_free_kbytes = 65536
net.ipv4.netfilter.ip_conntrack_max = 196608
net.netfilter.nf_conntrack_tcp_timeout_established = 7200
net.netfilter.nf_conntrack_checksum = 0
net.netfilter.nf_conntrack_max = 196608
net.netfilter.nf_conntrack_tcp_timeout_syn_sent = 15
net.nf_conntrack_max = 196608
net.ipv4.tcp_keepalive_time = 60
net.ipv4.tcp_keepalive_intvl = 10
net.ipv4.tcp_keepalive_probes = 3
net.ipv4.ip_local_port_range = 1025 65535
net.core.somaxconn = 262144
net.ipv4.tcp_max_tw_buckets = 2000000
net.ipv4.tcp_timestamps = 0

# sysctl fs.file-max
fs.file-max = 806854

# ulimit -n
500000

# cat /etc/security/limits.conf
*       soft    nofile 500000
*       hard    nofile 500000
