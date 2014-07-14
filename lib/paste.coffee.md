Paste
=====

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

            # Invoke the handler for any file types pasted
            [0...clipboardData.types.length].forEach (i) ->
              if file = clipboardData.items[i].getAsFile()
                handler file
