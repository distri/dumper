Dumper
======

Dump files and have them show up in S3.

    require "./lib/drop"
    require "./lib/paste"

    Stash = require "./stash"
    stash = Stash()

    Trinket = require "trinket"
    # TODO: Better way to get the policy
    trinket = Trinket(JSON.parse(localStorage.TRINKET_POLICY))

    handler = (file) ->
      console.log file
      # TODO: Add file to list of files
      
      sha = Trinket.SHA1(file)

      stash.add
        lastModifiedDate: file.lastModifiedDate
        size: file.size
        name: file.name
        type: file.type
        path: trinket.basePath() + sha
      # trinket.post file

    $("html").dropFile handler
    $(document).pasteFile handler
