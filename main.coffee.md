Dumper
======

Dump files and have them show up in S3.

    require "./lib/drop"

    Trinket = require "trinket"

    # TODO: Better way to get the policy
    trinket = Trinket(JSON.parse(localStorage.TRINKET_POLICY))

    handler = (file) ->
      console.log file
      # TODO: Add file to list of files
      trinket.post file

    $("html").dropFile handler

    # $(document).pasteImageReader handler
