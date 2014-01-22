require "pp"
require "rubygems"
require "json"
require "cgi"
require "net/http"
require "uri"

# slant.png workaround :\ https://github.com/henrik/hipchat-emoticons/pull/10
# Doubly escaped for Ruby + JS.
BOOKMARKLET = 'alert("Close this dialog and copy the URL, then go back to the terminal!"); re = new RegExp("^"+config.group_id+"/");' +
              'es = emoticons.emoticons.filter(function(x) { return !x.image.match(re) }).map(function(x) { delete x.regex; if (x.image == "slant.png") x.shortcut = ":\\\\"; return x; });' +
              'location.hash = JSON.stringify(es)'

desc "Updates custom.json."
task :default do

  token = ""
  url = "https://api.hipchat.com/v2/emoticon?auth_token=%s&type=group" % token
  cjson = Net::HTTP.get(URI.parse(url))
  cpretty = JSON.pretty_generate(cjson)
  cfile - "custom.json"
  puts cpretty
  File.open(cfile, "w") { |f| f.puts cpretty }
  puts "wrote to #{cfile}"

end

# desc "Updates emoticons.json."
# task :default do

#   IO.popen("pbcopy", "w") { |f| f << BOOKMARKLET }
#   puts "Copied bookmarklet to clipboard."

#   `open -g https://hipchat.com/chat`
#   puts "Opened chat in browser."
#   puts " * Log in if necessary."
#   puts " * Run the bookmarklet, do what it says."
#   print " * Hit Return when done:"
#   gets
#   raw_json = `pbpaste`.split('#', 2).last

#   # May contain HTML entities.
#   raw_json = CGI.unescapeHTML(raw_json)

#   json = JSON.parse(raw_json)

#   pretty = JSON.pretty_generate(json)

#   file = "emoticons.json"
#   puts pretty
#   File.open(file, "w") { |f| f.puts pretty }
#   puts "Wrote to #{file}."
# end

