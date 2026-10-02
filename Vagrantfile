# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Imagen base para todas las máquinas (Ubuntu 22.04 LTS)
  config.vm.box = "ubuntu/jammy64"

  # ==========================================
  # 1. SERVIDOR DHCP (dhcp)
  # ==========================================
  config.vm.define "dhcp" do |srv|
    srv.vm.hostname = "dhcp"

    # Adaptador 1: Red pública (Bridge con la red de tu host/casa/aula)
    srv.vm.network "public_network", bridge: "enp3s0"

    # Adaptador 2: Red interna 'intnet' con IP fija 192.168.57.10[cite: 2, 3]
    srv.vm.network "private_network",
      ip: "192.168.57.10",
      virtualbox__intnet: "intnet"
  end

  # ==========================================
  # 2. CLIENTE 1 (c1)
  # ==========================================
  config.vm.define "c1" do |c1|
    c1.vm.hostname = "c1"

    # Conectado a la red interna 'intnet' configurado por DHCP[cite: 2, 5]
    c1.vm.network "private_network",
      type: "dhcp",
      virtualbox__intnet: "intnet"
  end

  # ==========================================
  # 3. IMPRESORA (printer)
  # ==========================================
  config.vm.define "printer" do |printer|
    printer.vm.hostname = "printer"

    # Conectado a 'intnet' con una dirección MAC fija para asignación estática por DHCP[cite: 2, 7]
    printer.vm.network "private_network",
      :mac => "080027112233",
      type: "dhcp",
      virtualbox__intnet: "intnet"
  end

end