[[CGNAT]]

NAT (Network Address Translation) — это метод, используемый для изменения сетевых адресов в заголовках пакетов данных, проходящих через маршрутизатор или другое устройство сетевого оборудования. NAT используется для улучшения безопасности и уменьшения числа публичных IP-адресов, необходимых для организации сети.

Вот основные аспекты и виды NAT:

### Основные понятия

1. **Внутренние (частные) IP-адреса:**
    
    - Эти адреса используются в локальной сети (LAN) и не видны в интернете. Примеры: 192.168.x.x, 10.x.x.x, 172.16.x.x - 172.31.x.x.
    - Частные IP-адреса используются для устройств внутри локальной сети, таких как компьютеры, смартфоны и принтеры.
2. **Публичные IP-адреса:**
    
    - Эти адреса видны в интернете и используются для маршрутизации данных через интернет.
    - Публичные IP-адреса назначаются интернет-провайдерами и используются для идентификации устройств в глобальной сети.

### Как работает NAT

Когда устройство в локальной сети (например, компьютер) отправляет данные в интернет, NAT изменяет частный IP-адрес устройства на публичный IP-адрес маршрутизатора. Ответные данные также проходят через NAT, который заменяет публичный IP-адрес на частный, чтобы данные могли вернуться к устройству внутри локальной сети.

### Типы NAT

1. **Статический NAT (Static NAT):**
    
    - Каждый внутренний IP-адрес сопоставляется с фиксированным публичным IP-адресом.
    - Используется, когда требуется постоянный публичный IP-адрес для устройства внутри локальной сети (например, для веб-сервера).
2. **Динамический NAT (Dynamic NAT):**
    
    - Внутренние IP-адреса сопоставляются с публичными IP-адресами из пула доступных публичных адресов.
    - Используется для динамического назначения публичных IP-адресов внутренним устройствам, когда эти устройства выходят в интернет.
3. **PAT (Port Address Translation) или NAT Overload:**
    
    - Множество внутренних IP-адресов используют один публичный IP-адрес, но с разными номерами портов.
    - Это наиболее распространенная форма NAT, используемая в домашних и малых офисных сетях.
    - PAT позволяет экономить публичные IP-адреса и одновременно обеспечивает выход в интернет множеству устройств внутри локальной сети.

### Преимущества NAT

1. **Сокращение использования публичных IP-адресов:**
    
    - NAT позволяет множеству устройств в локальной сети использовать один публичный IP-адрес для доступа в интернет.
2. **Улучшение безопасности:**
    
    - Внутренние IP-адреса скрыты от внешнего мира, что затрудняет прямой доступ к устройствам внутри локальной сети.
3. **Гибкость в управлении сетью:**
    
    - NAT упрощает изменение внутренней структуры сети без необходимости изменения внешних (публичных) IP-адресов.

### Проблемы и ограничения NAT

1. **Проблемы с P2P и VoIP:**
    
    - Некоторые приложения, такие как пиринговые сети (P2P) и VoIP, могут испытывать трудности при работе через NAT, так как они требуют прямых соединений между устройствами.
2. **Сложность маршрутизации:**
    
    - NAT может добавить дополнительную задержку и нагрузку на маршрутизатор, так как он должен изменять IP-адреса и порты в каждом пакете данных.
3. **Требуется конфигурация проброса портов:**
    
    - Для доступа к внутренним устройствам из интернета нужно настроить проброс портов (port forwarding) на маршрутизаторе, что может быть сложным для некоторых пользователей.

NAT является важной частью современной сетевой инфраструктуры, предоставляя способ эффективного использования ограниченного пространства IPv4-адресов и улучшения безопасности сетей.