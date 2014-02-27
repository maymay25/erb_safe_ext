# erb_safe_ext

a gem make ERB html safe default.Protect from XSS attack.

## Install

```sh
$ gem install erb_safe_ext
```

## Introduction

``` ruby
<%= "<script>alert('safety:)');</script>" %>
## => &lt;script&gt;alert(&#x27;safety:)&#x27;);&lt;&#x2F;script&gt;
```

wrap the dangerous code with `Rack::Utils.escape_html(code)`

works fine with ruby2.1.

I didn't test this code with other version ruby, you may test yourself.

the `<%==` is the backup of ERB's original `<%=` function. 

``` ruby
<%== "<script>alert('danger!');</script>" %>
## => <script>alert('danger!');</script>
```


Test code

``` ruby
require 'erb_safe_ext'
template = ERB.new <<-EOF
<%= "<script>alert('safety:)');</script>" %>
<%#= 'here' -%>
<%== "<script>alert('danger!');</script>" %>
----finish----
EOF
puts template.result
```

