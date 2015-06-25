#MatchMediaMock [![Build Status](https://travis-ci.org/azazdeaz/match-media-mock.svg?branch=master)](https://travis-ci.org/azazdeaz/match-media-mock)
Simple server side compatible substitution for ```Window.matchMedia()``` based on [css-mediaquery].
Deisgned to use with [Radium].

###Basic usage
```javascript
var matchMediaMock = require('match-media-mock').create()
matchMediaMock.setConfig({type: 'screen', width: 1200})

matchMediaMock('(max-width: 991px)').matches // false
matchMediaMock('(max-width: 1240px)').matches // true

var mediaQueryList = matchMediaMock(mediaQuery)
mediaQueryList.addListener(listener)
mediaQueryList.removeListener(listener)
mediaQueryList.callListeners()
```

For more detailes about matching check out [css-mediaquery]!

###Example usage with [Radium]
```javascript
var Radium = require('radium')
var matchMediaMock = require('match-media-mock').create()
Radium.config.setMatchMedia(matchMediaMock)

app.get('/app/:width/:height', function(req, res) {
  matchMediaMock.setConfig({
    type: 'screen',
    width: req.params.width,
    height: req.params.height
  })
  var html = React.renderToString(<RadiumApp/>)
  res.end(html)
})
```
For more detailes see the [Radium docs][Radium]

[Radium]: https://github.com/FormidableLabs/radium/tree/master/docs/api#configsetmatchmedia
[css-mediaquery]: https://github.com/ericf/css-mediaquery
