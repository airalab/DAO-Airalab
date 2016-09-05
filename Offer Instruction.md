# Инструкция по созданию оферты на услуги в DAO Airalab

Для того, чтобы предложить услугу на рынке DAO, мы создадим специальный контракт `Offer`. Чтобы приступить к созданию оферты нам нужно иметь синхронизированный клиент Etherem сети - `Ethereum Wallet`, а также небольшое кол-во Ether на счету, для проведения транзакции.

Скачать его можно по ссылке, в разделе `Downloads`: [Ethereum Wallet](https://github.com/ethereum/mist/releases)

## Статусы кошелька

Если вы не знаете как определить, синхронизирован кошелек или нет, предлагаю скриншоты с описанием ниже:

### Не синхронизированный кошелек:

![Screenshot 1](/img/Screenshot_1.png)

Обращаем внимание на информацию между `Send` и `Contracts`. Там указано, по-порядку: количество пиров, количество загруженных блоков, время от последнего загруженного блока. Если у вас количество пиров равно 0, то для начала нужно подождать несколько минут. Ethereum использует пиринговые сети, подобно Torrent. На поиск пиров может уйти некоторое время. Если пиры не находятся, нужно, в первую очередь посмотреть не закрыт ли порт 30030, а также не установлены ли ограничения на пиринговые сети в вашей локальной сети. Или обратитесь к системному администратору.

### Кошелек в стадии синхронизации

![Screenshot 2](/img/Screenshot_2.png)

Если в поле информации появились `%` и шкала загрузки, то кошелек находится в процессе синхронизации. Этот процесс может занять много времени. Рекомендуется использовать систему с SSD, т.к. основная нагрузка идет на накопитель данных.

### Синхронизированный кошелек

![Screenshot 3](/img/Screenshot_3.png)

Когда шкала загрузки пропадет, и справа, в поле информации, можно будет увидеть отсчет в секундах от времени последнего блока, кошелек синхронизирован. В сети Ethereum блоки появляются в среднем, раз в 16 секунд. Обращайте внимание, на эту информацию. Если в поле отсчета от последнего блока будут цифры выше одной,двух минут, это может говорить о проблемах с соединением.

## Начало работы с DAO

### Добавление токенов

В этой инстукции будет описано как создать автономный контракт `Offer` в DAO Airalab. Т.к. любое DAO имеет свои внутренние токены-кредиты, используемые как средство расчета внутри DAO, нам нужно будет добавить их в список просматриваемых токенов. Для этого перейдем в раздел `Contracts`, кликнув по нему.

Список всех модулей DAO, включая токен `Credits`, хранится в контракте DAO Core, а также по адресу: [Airalab modules](https://github.com/airalab/DAO-Airalab)

Если вы знаете как работать с DAO Core, его адрес: `0xf38a9052cc162fab081dc8177a8f74a53f0da989`, [JSON interface](https://github.com/airalab/core/blob/master/abi/modules/Core.json), возмите адрес `Credits` оттуда. Если нет, с Github.

Сейчас нас интересует модуль `Credits`, его адрес - `0x4bc13752568B99036692bA8B1dB2c97d6Df457f4`

Чтобы добавить токен `Credits` в список наблюдаемых, нажмем кнопку `Watch Token` внизу раздела `Contracts`.

![Screenshot 4](/img/Screenshot_4.png)

Затем, вставим адрес `Credits` в строку `TOKEN CONTRACT ADDRESS`.

![Screenshot 5](/img/Screenshot_5.png)

Таким же образом добавим хранилище Ether, `Ether Leger`, его адрес `0x15d2b79ded1dd856070fc68e9ff4c1896934b14f`

### Добавление автономных контрактов

После того, как оферта будет принята, создателю оферты будут перечислены AIR, внутренние токены Airalab DAO. Их нужно будет поменять на Ether, для этого в Airalab DAO существует модуль `Market`. На нем можно обменивать токены. Адрес `Market` хранится в DAO Core. Если вы не знаете как работать с DAO Core, привожу адрес ниже:
`0xFE7D3D1b1749863F8a3F24c9ACC0AF282109F416`, [JSON interface](https://raw.githubusercontent.com/airalab/core/master/abi/modules/Market.json)

Добавим автономный контракт `Market` в список наблюдаемых. Для этого нажмем кнопку `Watch contract` в разделе `Contracts`.

![Screenshot 6](/img/Screenshot_6.png)

Назовем его `Airalab Market`, вставим адрес и JSON interface, указанные выше. Контракт появится в списке наблюдаемых.

Далее, нам необходимо добавить автономный контракт `OfferBuilder`, который создаст для нас оферту по выбранным параметрам. `OfferBuilder` - это модуль другого DAO, `DAO Factory`. Как с ним работать было описано в учебном центре. Сейчас на нем подробно останавливаться не будем.  
Адрес и JSON interface OfferBuilder:

Address: `0xF56a5Df46AE71f7465c44AfBc2E3277D22f778eD`  
JSON:
``` js
[ { "constant": false, "inputs": [ { "name": "_uri", "type": "string" } ], "name": "setSecurityCheck", "outputs": [], "type": "function" }, { "constant": false, "inputs": [ { "name": "_beneficiary", "type": "address" } ], "name": "setBeneficiary", "outputs": [], "type": "function" }, { "constant": true, "inputs": [], "name": "beneficiary", "outputs": [ { "name": "", "type": "address", "value": "0x2e3e8f5dac79e49e199e86f4226511261e3704dd" } ], "type": "function" }, { "constant": false, "inputs": [], "name": "kill", "outputs": [], "type": "function" }, { "constant": false, "inputs": [ { "name": "_buildingCostWei", "type": "uint256" } ], "name": "setCost", "outputs": [], "type": "function" }, { "constant": false, "inputs": [ { "name": "_owner", "type": "address" } ], "name": "delegate", "outputs": [], "type": "function" }, { "constant": true, "inputs": [], "name": "buildingCostWei", "outputs": [ { "name": "", "type": "uint256", "value": "100000000000000000" } ], "type": "function" }, { "constant": true, "inputs": [], "name": "owner", "outputs": [ { "name": "", "type": "address", "value": "0x4af013afbadb22d8a88c92d68fc96b033b9ebb8a" } ], "type": "function" }, { "constant": true, "inputs": [], "name": "getLastContract", "outputs": [ { "name": "", "type": "address", "value": "0x" } ], "type": "function" }, { "constant": true, "inputs": [ { "name": "", "type": "address" }, { "name": "", "type": "uint256" } ], "name": "getContractsOf", "outputs": [ { "name": "", "type": "address", "value": "0x" } ], "type": "function" }, { "constant": true, "inputs": [], "name": "securityCheckURI", "outputs": [ { "name": "", "type": "string", "value": "" } ], "type": "function" }, { "constant": false, "inputs": [ { "name": "_description", "type": "string" }, { "name": "_token", "type": "address" }, { "name": "_value", "type": "uint256" }, { "name": "_beneficiary", "type": "address" }, { "name": "_hard_offer", "type": "address" } ], "name": "create", "outputs": [ { "name": "", "type": "address" } ], "type": "function" }, { "anonymous": false, "inputs": [ { "indexed": true, "name": "sender", "type": "address" }, { "indexed": true, "name": "instance", "type": "address" } ], "name": "Builded", "type": "event" } ]
```

Добавим его список наблюдаемых контрактов, таким же способом, что и `Market`.

## Создание оферты

Чтобы создать оферту, нам необходимо обратиться в сбощик `OfferBuilder`, который мы добавили в предыдущей части инструкции. Для это кликнем по нему. Откроется окно контракта.

![Screenshot 7](/img/Screenshot_7.png)

Нас интересует раздел `Write to contract`. Выберем в выпадающем списке функцию `Create`, для создания оферты. Заполняем:  
     description - описание вашей услуги  
     token - адрес токена, который вы хотите получить, в нашем случае, это AIR (Airalab Credits)  
     value - кол-во токенов, стоимость услуги  
     beneficiary - адрес, на который пойдут токены после принятия оферты  
     hard_offer - в этом поле можно указать адрес для которого создается оферта. При таком указании оферта становится твердой и может быть принята только с указанного адреса

Сборщик контрактов берет комиссию за свои услуги. Её размер указан в разделе `Read from contract`, в поле `Building cost wei`. Величина указана в wei и в данном случае равна 0.1 Eth. Эту сумму необходимо добавить к транзакции. Далее нажимаем кнопку `Execute`.

После того, как транзакция будет замайнена и сборщик сделает контракт, его адрес можно будет посмотреть в контракте `OfferBuilder` в разделе `Latest Events`. Вам нужно найти адрес своего кошелька в списке `Sender`, под ним будет указан адрес созданной оферты в графе `Instance`. Этот адрес нужно передать клиенту.
