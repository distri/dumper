Paste
=====

TODO: This isn't so simple as the file dropping :(

    do ($=jQuery) ->
      $.event.fix = do (originalFix=$.event.fix) ->
        (event) ->
          event = originalFix.apply(this, arguments)

          if event.type.indexOf('copy') == 0 || event.type.indexOf('paste') == 0
            event.clipboardData = event.originalEvent.clipboardData

          return event

      $.fn.pasteFile = (handler) ->
        @each ->
          element = this
          $this = $(this)

          $this.bind 'paste', (event) ->
            clipboardData = event.clipboardData
            console.log "pasted!"
            debugger
            [0...clipboardData.types.length].forEach (i) ->
              console.log clipboardData.items[i].getAsFile()

            # TODO: Handle other types?
            # handler clipboardData.items[0]
