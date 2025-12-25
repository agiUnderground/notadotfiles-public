`privacy.resistFingerprinting` - enable to randomize html headers like timezone, os, display size etc. (about:config)

`pdfjs.enableScripting` [false] - disable javascript when viewing PDFs in firefox.

`dark mode in pdf viewer(add as a url in a bookmark)` - 
```
javascript:(function(){var el = typeof viewer !== 'undefined' ? viewer : document.body; el.style = 'filter: grayscale(1) invert(1) sepia(1) contrast(75%)'; document.body.style.background = "black";})()
```

`network.dns.echconfig.enabled` [true]- ESNI enable(server name identification).

`network.dns.http3_echconfig.enabled` [true] - ESNI enable.

disable jit
```
javascript.options.baselinejit = false
javascript.options.ion = false
javascript.options.wasm = false ?????
javascript.options.asmjs = false
javascript.options.wasm_baselinejit = false
javascript.options.wasm_optimizingjit = false // can break some websites etc
```

network.http.referer.XOriginPolicy

```
    controls whether or not to send a referrer across origins
    values:
        0 = (default) send the referrer in all cases
        1 = send a referrer only when the base domains are the same
        2 = send a referrer only on same-origin
```

`extensions.pocket.enabled` = false

`geo.enabled` = false

`dom.battery.enabled` = false  // Disable Battery Status API

`media.webspeech.synth.enabled` = false

Check the FPS of the UI renderer:

```
What you are describing is the old deprecated performance profiler,
the new one does not display fps. You can see fps in the UI by going to
about:config and changing gfx.webrender.debug.profiler-ui to FPS and
gfx.webrender.debug.profiler to true.
```

```layout.frame_rate``` - Change framerate hardcap?


Change `gfx.display.frame-rate-divisor` to `2` to make `FPS 30` instead of default `60`.
```
# Rate by which the frame rate is divided. I.e. at a number higher than 1 we
# will only refresh every <x> frames.
- name: gfx.display.frame-rate-divisor
  type: RelaxedAtomicInt32
  value: 1
  mirror: always
```

All about Firefox framerates - https://searchfox.org/mozilla-release/source/modules/libpref/init/StaticPrefList.yaml


```
image.animation_mode = none
toolkit.cosmeticAnimations.enabled = false
```

Disable AI shit(set it to false):
```
    browser.ml.enable
    browser.ml.chat.enabled
    browser.ml.chat.menu
    browser.ml.chat.page
    browser.ml.chat.page.footerBadge
    browser.ml.chat.page.menuBadge
    browser.ml.linkPreview.enabled
    browser.ml.pageAssist.enabled
    browser.tabs.groups.smart.enabled
    browser.tabs.groups.smart.userEnabled
    extensions.ml.enabled
    browser.search.visualSearch.featureGate
    extensions.ui.mlmodel.hidden
```

