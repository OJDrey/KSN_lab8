# Лабораторна робота №8 — Vagrantfile (Варіант 18)

Vagrant.configure("2") do |config|
  # Образ ОС під Варіант 18 (AlmaLinux 9)
  config.vm.box = "generic/alma9"

  # Назва хоста всередині ВМ
  config.vm.hostname = "alma9-lab8"

  # Прокидання порту 80 гостя на порт 8080 хоста
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Синхронізована папка проєкту
  config.vm.synced_folder ".", "/vagrant"

  # Налаштування ресурсів у VirtualBox (1024 МБ ОЗУ, 1 CPU)
  config.vm.provider "virtualbox" do |vb|
    vb.name   = "alma9-lab8-var18"
    vb.memory = 1024
    vb.cpus   = 1
  end

  # Автоматичне встановлення та запуск Nginx (AlmaLinux використовує пакетний менеджер dnf)
  config.vm.provision "shell", inline: "dnf install -y nginx && systemctl enable --now nginx && systemctl stop firewalld"
end