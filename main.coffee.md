Dumper
======

    # TODO: Update editor hamlet and fix this required global
    global.Observable = require "observable"

Dump files and have them show up in S3.

    {applyStylesheet} = require "util"
    applyStylesheet require "./style"

    require "./lib/drop"
    require "./lib/paste"

    Stash = require "./stash"
    stash = Stash()

    Trinket = require "trinket"
    # TODO: Better way to get the policy
    # maybe from location.hash?
    trinket = Trinket(JSON.parse(localStorage.TRINKET_POLICY))

    handler = (file) ->
      console.log file
      # TODO: Add file to list of files

      trinket.post file

      Trinket.SHA1 file, (sha) ->
        stash.push
          lastModifiedDate: file.lastModifiedDate
          size: file.size
          name: file.name
          type: file.type
          path: trinket.basePath() + sha

    $("html").dropFile handler
    $(document).pasteFile handler

    document.body.appendChild require("./files")
      files: stash
