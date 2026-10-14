# Звіт з лабораторної роботи №8
**Тема:** Ознайомлення з системою Vagrant

## Вихідні дані
- ПІБ: Репета Андрій Назарович
- Група: КІ-405п
- Варіант (має збігатися з variant.txt):18

## 1. Версії встановленого ПЗ
Вставте вивід команд:

```text
$ vagrant --version
Vagrant 2.4.9

$ VBoxManage --version
7.2.20r175154
```

## 2. Гостьова система
Вивід команд усередині ВМ (`vagrant ssh`):

```text
$ cat /etc/os-release
NAME="AlmaLinux"
VERSION="9.3 (Shamrock Pampas Cat)"
ID="almalinux"
ID_LIKE="rhel centos fedora"
VERSION_ID="9.3"
PLATFORM_ID="platform:el9"
PRETTY_NAME="AlmaLinux 9.3 (Shamrock Pampas Cat)"
ANSI_COLOR="0;34"
LOGO="fedora-logo-icon"
CPE_NAME="cpe:/o:almalinux:almalinux:9::baseos"
HOME_URL="https://almalinux.org/"
DOCUMENTATION_URL="https://wiki.almalinux.org/"
BUG_REPORT_URL="https://bugs.almalinux.org/"

ALMALINUX_MANTISBT_PROJECT="AlmaLinux-9"
ALMALINUX_MANTISBT_PROJECT_VERSION="9.3"
REDHAT_SUPPORT_PRODUCT="AlmaLinux"
REDHAT_SUPPORT_PRODUCT_VERSION="9.3"

$ free -h
               total        used        free      shared  buff/cache   available
Mem:           949Mi       335Mi       503Mi       5.0Mi       258Mi       614Mi
Swap:          2.0Gi          0B       2.0Gi

$ df -h
Filesystem                        Size  Used Avail Use% Mounted on
devtmpfs                          4.0M     0  4.0M   0% /dev
tmpfs                             475M     0  475M   0% /dev/shm
tmpfs                             190M  5.6M  185M   3% /run
/dev/mapper/almalinux_alma9-root   70G  2.4G   68G   4% /
/dev/sda1                         960M  177M  784M  19% /boot
vagrant                           244G  151G   93G  62% /vagrant
tmpfs                              95M     0   95M   0% /run/user/1000
```

## 3. Виконані команди керування
Для кожної команди вставте її вивід (або фрагмент) і скріншот у папку `screenshots/`.

```text
vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'generic/alma9' version '4.3.12' is up to date...
==> default: Resuming suspended VM...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
-vagrant ssh
Last login: Wed Oct 14 15:46:51 2026 from 10.0.2.2
[vagrant@alma9-lab8 ~]$ 
vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
-vagrant halt
==> default: Attempting graceful shutdown of VM...
-vagrant reload
==> default: Checking if box 'generic/alma9' version '4.3.12' is up to date...
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 80 (guest) => 8080 (host) (adapter 1)
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default:
    default: Guest Additions Version: 6.1.48
    default: VirtualBox Version: 7.2
==> default: Setting hostname...
==> default: Mounting shared folders...
    default: E:/Vagrant/lab8_v18 => /vagrant
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
-vagrant provision
==> default: Running provisioner: shell...
    default: Running: inline script
    default: Extra Packages for Enterprise Linux 9 - x86_64   48 kB/s |  13 kB     00:00
    default: Package nginx-2:1.20.1-28.el9_8.6.alma.1.x86_64 is already installed.
    default: Dependencies resolved.
    default: Nothing to do.
    default: Complete!
-vagrant snapshot save lab8
==> default: Snapshotting the machine as 'lab8'...
==> default: Snapshot saved! You can restore the snapshot at any time by
==> default: using `vagrant snapshot restore`. You can delete it using
==> default: `vagrant snapshot delete`.
-vagrant box list
bento/ubuntu-22.04 (virtualbox, 202510.26.0, (amd64))
generic/alma9      (virtualbox, 4.3.12, (amd64))
-vagrant global-status
id       name    provider   state   directory
------------------------------------------------------------------------
5cdb479  default virtualbox running E:/Vagrant/lab8_v18

The above shows information about all known Vagrant environments
on this machine. This data is cached and may not be completely
up-to-date (use "vagrant global-status --prune" to prune invalid
entries). To interact with any of the machines, you can go to that
directory and run Vagrant, or you can use the ID directly with
Vagrant commands from any directory. For example:
"vagrant destroy 1a2b3c4d"
-vagrant destroy
    default: Are you sure you want to destroy the 'default' VM? [y/N] N
==> default: The VM 'default' will not be destroyed, since the confirmation
==> default: was declined.

```
(замініть цей блок реальним виводом)

## 4. Пояснення Vagrantfile
Поясніть кожен рядок вашого Vagrantfile:

* `Vagrant.configure("2") do |config|` — Ініціалізує блок конфігурації Vagrant з використанням версії API 2.x.
* `config.vm.box = "generic/alma9"` — Задає базовий образ операційної системи AlmaLinux 9 під Варіант 18.
* `config.vm.hostname = "alma9-lab8"` — Встановлює системне ім'я хоста всередині гостьової віртуальної машини.
* `config.vm.network "forwarded_port", guest: 80, host: 8080` — Налаштовує прокидання порту: вхідні запити на порт 8080 хоста перенаправляються на порт 80 ВМ.
* `config.vm.synced_folder ".", "/vagrant"` — Налаштовує спільну папку: поточний каталог проєкту на хості монтується за шляхом `/vagrant` у ВМ.
* `config.vm.provider "virtualbox" do |vb|` — Відкриває блок специфічних налаштувань для провайдера віртуалізації VirtualBox.
* `vb.name = "alma9-lab8-var18"` — Задає відображуване ім'я віртуальної машини в інтерфейсі VirtualBox.
* `vb.memory = 1024` — Виділяє 1024 МБ (1 ГБ) оперативної пам'яті для ВМ.
* `vb.cpus = 1` — Виділяє 1 ядро процесора для віртуальної машини.
* `end` — Завершує блок налаштувань провайдера VirtualBox.
* `config.vm.provision "shell", inline: "dnf install -y nginx &amp;&amp; systemctl enable --now nginx &amp;&amp; systemctl stop firewalld"` — Автоматично завантажує та встановлює вебсервер Nginx через dnf, запускає його сервіс та вимикає брандмауер для відкриття порту 80.
* `end` — Завершує головний блок конфігурації Vagrant.

## 5. Висновки
Під час виконання лабораторної роботи №8 було успішно опановано інструмент Vagrant для створення та управління відтворюваними середовищами розробки на базі VirtualBox. Було розгорнуто та налаштовано віртуальну машину AlmaLinux 9 за варіантом 18, сконфігуровано прокидання портів (8080 -&gt; 80), ресурси (1024 МБ RAM, 1 CPU) та реалізовано автоматичне встановлення й запуск вебсервера Nginx за допомогою shell-провіженера.

## 6. Контрольні запитання

### Питання 1
Що таке Vagrant? Для яких завдань його використовують?

**Vagrant - це інструмент командного рядка для автоматизації створення та налаштування відтворювальних середовищ розробки поверх гіпервізорів віртуалізації (наприклад, VirtualBox). Його використовують для швидкого розгортання ізольованих ВМ, забезпечення однаковості конфігурацій середовища для всієї команди розробників та тестування ПЗ.**

### Питання 2
Що таке Docker і чим контейнер відрізняється від віртуальної машини?

**Docker - це платформа контейнеризації для запуску додатків в ізольованих контейнерах. Віртуальна машина запускає повноцінну гостьову ОС із власним ядром та потребує більше ресурсів, тоді як контейнер Docker використовує спільне ядро ОС хоста, є значно легшим та запускається за декілька секунд.**

### Питання 3
Якою мовою написано Vagrant і якою мовою описується Vagrantfile?

**Сам інструмент Vagrant написано мовою програмування Ruby. Конфігураційний файл Vagrantfile також описується мовою Ruby DSL (Domain Specific Language), що дозволяє використовувати внутрішній синтаксис та структури Ruby для гнучкого налаштування параметрів ВМ.**

### Питання 4
Як встановити Vagrant у вашій ОС? Які ще компоненти потрібні?

**У ОС Windows або macOS Vagrant встановлюється за допомогою офіційного інсталяційного пакета MSI/DMG, завантаженого з сайту HashiCorp. Додатково потрібен провайдер віртуалізації (наприклад, Oracle VirtualBox), увімкнена апаратна віртуалізація (VT-x/AMD-V) у BIOS/UEFI та клієнт SSH.**

### Питання 5
Який протокол використовується для підключення до гостьової системи і який порт хоста за замовчуванням?

**Для підключення до гостьової системи використовується протокол безпечного мережевого доступу SSH (команда `vagrant ssh`). За замовчуванням стандартний порт SSH віртуальної машини (22) перенаправляється на порт 2222 локального хоста (127.0.0.1).**

### Питання 6
Що таке box і де знайти готові образи?

**Box - це попередньо скомпонований базовий образ операційної системи (наприклад, AlmaLinux чи Ubuntu), який завантажується та використовується як шаблон для створення ВМ. Готові офіційні та користувацькі образи можна знайти в публічному хмарному каталозі Vagrant Cloud (app.vagrantup.com).**

### Питання 7
Яке призначення Vagrantfile? Які параметри в ньому можна задати?

**Vagrantfile призначений для опису конфігурації віртуального середовища проєкту. У ньому задають базовий образ (box), назву хоста, мережеві параметри (прокидання портів), обсяг ОЗУ та CPU, спільні папки (synced\_folder) та скрипти автоматичного налаштування ПЗ (provision).**

### Питання 8
У чому різниця між `vagrant halt`, `vagrant suspend` та `vagrant destroy`?

**Команда `vagrant halt` коректно вимикає гостьову ОС зі збереженням стану диска. Команда `vagrant suspend` призупиняє робочий стан ВМ із дампом оперативної пам'яті на диск для швидкого відновлення. Команда `vagrant destroy` повністю видаляє ВМ та її віртуальні диски з ПК.**

### Питання 9
Для чого `vagrant provision` та `vagrant reload`? Коли використовувати кожну?

**Команда `vagrant reload` перезапускає ВМ із повторним зчитуванням змін конфігурації з Vagrantfile (потрібна при зміні портів чи ресурсів). Команда `vagrant provision` повторно виконує лише скрипти встановлення та налаштування ПЗ без перезапуску самої ВМ.**

### Питання 10
Що таке synced folder і який каталог ВМ відповідає каталогу проєкту?

**Synced folder (синхронізована папка) — це механізм автоматичного обміну файлами між хостовою операційною системою та віртуальною машиною. За замовчуванням поточний робочий каталог проєкту з хостового ПК монтується всередині ВМ за шляхом `/vagrant`.**
