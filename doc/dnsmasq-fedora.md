# Install Dnsmasq

Install dnsmasq package

    > dnf install dnsmasq

Open dns port in firewalld

    > firewall-cmd --zone=public --permanent --add-service=dns
