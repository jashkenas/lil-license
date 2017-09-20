# Handy shcortcut to build live as you work:
# fswatch -o LICENSE README | xargs -n1 -I{} cake build

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
  faq    = fs.readFileSync('README').toString()
  v1     = fs.readFileSync('v1.html').toString()

  v1 = v1.replace matcher('lil-license'), section('lil-license', wrap(source))
  v1 = v1.replace matcher('faq'), section('faq', md.render(faq))

  fs.writeFileSync 'v1.html', v1
