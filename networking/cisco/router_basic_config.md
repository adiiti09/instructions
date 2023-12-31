
    hostname csr01

    ip domain-name example.com

    username admin privilege 15 secret cisco

    crypto key generate rsa modulus 2048

    line vty 0 15
        transport input ssh
        login local

    write memory

    copy running-config startup-config

