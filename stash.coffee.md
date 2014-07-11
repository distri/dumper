Stash
=====

Store a list of file metada with pointers to an S3 CAS bucket.

    module.exports = (name) ->
      add: (data) ->
        items JSON.parse(localStorage[name] || "[]").push data
        localStorage[name] = JSON.stringify(items())
      remove: () ->
      