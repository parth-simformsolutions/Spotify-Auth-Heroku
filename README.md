# Spotify Auth Heroku
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.png?v=103)][mitLink]

## About
Quick and easy deployment to Heroku to enable access to Spotify's WEB API through user authentication:

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/kevinjnguyen/Spotify-Auth-Heroku/tree/master)

Your application must follow the Spotify authentication process:
* Your web application must perform a GET request to Spotify's Authorize endpoint. e.g.
    ```
    app.get('/login', function(req, res) {
    var scopes = 'user-read-private user-read-email';
    res.redirect('https://accounts.spotify.com/authorize' +
    '?response_type=code' +
    '&client_id=' + my_client_id +
    (scopes ? '&scope=' + encodeURIComponent(scopes) : '') +
    '&redirect_uri=' + encodeURIComponent(redirect_uri));
    });
    ```
    The `redirect_uri` is the Heroku application url.
* The Heroku application will take the access token granted by the user and exchange it for a session token which is used for requests.
* This application will handle the callback and token exchange then return to a redirect to a new webpage with the new token for use.

## Environmental Variables
Clicking the "deploy to heroku" button will prompt you for these variables:
* `CLIENT_ID` - Spotify Application Client ID *Required*
* `CLIENT_SECRET` - Spotify Application Client Secret *Required*
* `CALLBACK_URL` - The application Spotify returns authentication back to. This is the Heroku application URL. *Required*
* `REDIRECT_URL` - After exchanging the access token for a session token, redirect to this url to `<URL>/<session_token>`.

## License

`Spotify-Auth-Heroku` is released under an [MIT License][mitLink].

**Copyright &copy; 2019-present Kevin J Nguyen.**

*Please provide attribution, it is greatly appreciated.*

[mitLink]:http://opensource.org/licenses/MIT