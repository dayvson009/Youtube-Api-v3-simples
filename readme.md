# Api Youtube  v3 Simples
---

[Api Youtube v3](https://developers.google.com/youtube/v3/code_samples/javascript) 


Para conseguir o Id você pode entrar nesse link do própio youtube [https://www.youtube.com/account_advanced](https://www.youtube.com/account_advanced)

ou entrando na seguinte página [Get my YouTube ID](http://mpgn.github.io/YTC-ID/) , e escrever o nome do usuario

---
## Vou mostrar de uma forma simples como ultilizar o Api do Youtube v3.

HTML :

``` html
<!DOCTYPE html>
<html>
<head>
<script src="//code.jquery.com/jquery-2.1.1.min.js"></script>
<script src="https://apis.google.com/js/client.js?onload=init"></script>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
    <script src="https://apis.google.com/js/client.js?onload=googleApiClientReady"></script>
</body>
</html>
  
```


Javascript:

``` javascript
function googleApiClientReady() {

    var apiKey = 'AIzaSyCZfHRnq7tigC-COeQRmoa9Cxr0vbrK6xw';

    gapi.client.setApiKey(apiKey);
    gapi.client.load('youtube', 'v3', function() {

        request = gapi.client.youtube.search.list({
            part: 'id, snippet',
            channelId: 'UCBN8Rqu2nSsXX_6UCZp5jLQ',
            order: 'date',
            type: 'video',
            maxResults: '40'

        });

        request.execute(function(response) {
          console.log(response);
          getThumbnails(response);
        });

    });

}
  
```

### O resultado mostrará no console;

## No código abaixo eu criei uma função para me retornar as Imagens e o link do youtube:

Código Completo :


``` html
  <!DOCTYPE html>
<html>
<head>
<script src="//code.jquery.com/jquery-2.1.1.min.js"></script>
<script src="https://apis.google.com/js/client.js?onload=init"></script>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>

  <div id="thumbnail"></div>
  <script>

function googleApiClientReady() {

    var apiKey = 'AIzaSyCZfHRnq7tigC-COeQRmoa9Cxr0vbrK6xw';

    gapi.client.setApiKey(apiKey);
    gapi.client.load('youtube', 'v3', function() {

        request = gapi.client.youtube.search.list({
            part: 'id, snippet',
            channelId: 'UCBN8Rqu2nSsXX_6UCZp5jLQ',
            order: 'date',
            type: 'video',
            maxResults: '40'

        });

        request.execute(function(response) {
          getThumbnails(response.items);
        });

        function getThumbnails(item) {

          elementLink = document.querySelector('#thumbnail')

          for (var i = 0; i < item.length; i++) {

            elementLink.innerHTML += '<a href="https://www.youtube.com/watch?v='+item[i].id.videoId+'">'+item[i].id.videoId+'</a><br>';
            elementLink.innerHTML += '<img src="'+item[i].snippet.thumbnails.default.url+'"><br>';
            elementLink.innerHTML += '<img src="'+item[i].snippet.thumbnails.high.url+'"><br>';
            elementLink.innerHTML += '<img src="'+item[i].snippet.thumbnails.medium.url+'"><br>';

          };
        };

    });

}
  </script>
    <script src="https://apis.google.com/js/client.js?onload=googleApiClientReady"></script>
</body>
</html>
```