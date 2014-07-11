Drop
====

Pass dropped files dropped on an element to a handler.

    do ($=jQuery) ->
      $.event.fix = do (originalFix=$.event.fix) ->
        (event) ->
          event = originalFix.apply(this, arguments)

          if event.type.indexOf('drag') == 0 || event.type.indexOf('drop') == 0
            event.dataTransfer = event.originalEvent.dataTransfer

          event

      stopFn = (event) ->
        event.stopPropagation()
        event.preventDefault()

      $.fn.dropFile = (handler) ->
        @each ->
          element = this
          $this = $(this)

          $this.on 'dragenter dragover dragleave', stopFn

          $this.on 'drop', (event) ->
            stopFn(event)

            Array::forEach.call event.dataTransfer.files, (file) ->    
              handler file
