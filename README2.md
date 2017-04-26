## Installation(安装)
This is a Node.js module available through the npm registry. Installation is done using the npm install command:
这是一个node.js的模块,已经通过npm注册,安装使用npm安装命令完成:
<pre><code>$ npm install express-session
</code></pre>
(window下请无视$)
----------------------------------------------------------------------------------------------------------------
## API
<pre><code>var session = require('express-session')</pre></code>
session(options)
Create a session middleware with the given options.
使用给定的选项创建一个会话中间件
Note Session data is not saved in the cookie itself, just the session ID. Session data is stored server-side.
注意:会话数据不是保存在他自己的cookie当中,cookie当中仅有一个session ID,会话数据是存储于服务端.
Note Since version 1.5.0, the cookie-parser middleware no longer needs to be used for this module to work. This module now directly reads and writes cookies on req/res. Using cookie-parser may result in issues if the secret is not the same between this module and cookie-parser.
注意:自版本1.5.0以后,这个模块在使用的使用不再需要使用cookie-parser中间件。现在这个模块直接在req/res的时候读取和写入cookie。如果当前模块和cookie-parser之间的加密是不一样的,使用cookie-parser可能导致问题.
Warning The default server-side session storage, MemoryStore, is purposely not designed for a production environment. It will leak memory under most conditions, does not scale past a single process, and is meant for debugging and developing.
警告:默认服务器端会话存储,内存存储,故意不用于生产环境。在大多数情况下它会泄漏内存,不存在缩小部分在一个单线程,用于调试和开发。
For a list of stores, see compatible session stores.
关于这个存储的列表,请参阅会话存储兼容.
Options
express-session accepts these properties in the options object.
express-session接受这些属性的选择对象。
