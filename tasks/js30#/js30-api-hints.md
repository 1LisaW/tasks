## js30-api-hints.md
Советы по выполнению 4-6 части задания js-30:
- [random-jokes](js30-4.md)
- [image-galery](js30-5.md)
- [movie-app](js30-6.md)

1. [Asynchronous JavaScript](#asynchrony-in-js)
2. [API](#api)
3. [](#)
4. [](#)
5. [](#)
6. [](#)
7. [](#)

### Asynchronous JavaScript

Частая задача в веб-разработке - получение данных от сервера и их отображение на веб-странице. Это могут быть курсы валют, данные о погоде, обзоры новостей, любая другая информация, которая должна динамически обновляться.

Особенность получения информации от сервера в том, что это очень длительный по времени процесс, по сравнению с выполнением другой части js-кода, и его результат заранее неизвестен: данные могут прийти, или не прийти, или прийти, но позже.

Для аналогии используем жизненную ситуацию - ожидание самолёта в аэропорту.  
По расписанию самолёт должен быть, но пока его не подадут на взлётную площадку, мы не можем быть уверены, что вылет состоится причём в точно указанное время.

В JavaScript код выполняется так, как он написан, срочка за строчкой. Это - поток кода. Но выполнять получение данных от сервера в основном потоке было бы нерационально: это тормозило бы код, пользователь был бы вынужден ждать пока может быть придут данные, а если бы данные не пришли, выполнение кода останавливалось бы, и приложение прекращало свою работу.

Так появился Асинхронный JavaScript (Asynchronous JavaScript), в котором код для получения данных от сервера добавляется в очередь и выполняется только после выполнения основного потока кода.

#### Историческая справка

В истории веб-разработки сначала получение новых данных от сервера предполагало перезагрузку всей страницы. Затем пришло понимание, что было бы хорошо получать данные без перезагрузки. Так появился AJAX (англ. Asynchronous JavaScript and XML). Асинхронный JavaScript код для получения данных от сервера откладывает в очередь и выполняет только после выполнения основного потока кода.

Технологии, которые при этом используются, - XMLHttpRequest (появилась около 30 лет назад), позже Fetch. На сегодня новейшим и наиболее удобным способом получения данных с сервера является функция `async/await`.

Функция `async/await` это синтаксический сахар над Fetch. Она позволяет писать асинхронный код почти так же просто и удобно, как если бы мы писали обычный js-код.

### API

API это источник данных, которые можно получить по запросу  
Примеры API
- OpenWeatherMap API - данные о погоде в населённом пункте
- MapBox API - карты
- OpenCage Geocoder - координаты по названию населённого пункта и названия населённых пунктов по координатам 
- Unsplash API и Flickr API - изображения на указанную тему

### Unsplash API
- сайт: https://unsplash.com/developers
- документация: https://unsplash.com/documentation
- у данного сервиса есть лимит - 50 изображений в час
- регистрируемся на сайте
- подтверждаем email (переходим по ссылке, которая пришла на почту)
- создаём приложение `https://unsplash.com/oauth/applications`
- получаем Access Key
- генерируем ссылку:  
`https://api.unsplash.com/photos/random?orientation=landscape&query=nature&client_id=e2077ad31a806c894c460aec8f81bc2af4d09c4f8104ae3177bb809faf0eac17`  
В ней:  
  - `orientation=landscape` - фото вытянутое по горизонтали
  - `query=nature` - запрос, по которому ищем фото
  - `client_id=` - Access Key, у вас будет другой.

Для удобного просмотра результатов, которые возвращает API, установите расширение [JSONView](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc?hl=ru)

Асинхронная функция, позволяющия получить ссылку на изображение в большом размере:  
```js
 async function getLinkToImage() {
   const url = 'https://api.unsplash.com/photos/random?query=morning&client_id=e2077ad31a806c894c460aec8f81bc2af4d09c4f8104ae3177bb809faf0eac17';
   const res = await fetch(url);
   const data = await res.json();
   console.log(data.urls.regular)
 }
  ```

Обратите внимание, что `async/await` функции работают только на сервере. Live Server (расширение VS Code) подойдёт.
