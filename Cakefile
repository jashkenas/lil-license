# Handy shcortcut to build live as you work:
# fswatch -o LICENSE FAQ.md | xargs -n1 -I{} cake build

fs = require 'fs'
md = require('markdown-it')()

wrap = (parts) ->
  body = parts.slice(1).map((part) -> "<p>#{part}</p>").join('\n\n')
  "\n\n<h1>#{parts.shift()}</h1>\n\n#{ body }\n\n"

section = (name, html) ->
  "<div class=\"#{name}\">#{html}</div>"

matcher = (name) ->
  ///<div\sclass="#{name}">[\s\S]*?<\/div>///

task 'build', 'build the HTML source from the LICENSE file', ->
  source = fs.readFileSync('LICENSE').toString().split(/\n{2,}/g)
  faq    = fs.readFileSync('FAQ.md').toString()
  index  = fs.readFileSync('index.html').toString()

  index = index.replace matcher('lil-license'), section('lil-license', wrap(source))
  index = index.replace matcher('faq'), section('faq', md.render(faq))

  fs.writeFileSync 'index.html', index
