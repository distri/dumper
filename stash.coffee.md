Stash
=====

    Observable = require "observable"

Store a list of file metada with pointers to an S3 CAS bucket.

    module.exports = (name) ->
      items = Observable []

      items JSON.parse(localStorage[name] || "[]")

      items.observe (newItems) ->
        localStorage[name] = JSON.stringify(newItems)

      items
