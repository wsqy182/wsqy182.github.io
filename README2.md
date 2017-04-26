## Installation(安装)
This is a Node.js module available through the npm registry. Installation is done using the npm install command:
 
这是一个node.js的模块,已经通过npm注册,安装使用npm安装命令完成:
```
$ npm install express-session
```
(window下请无视$)

---
## API
```
var session = require('express-session')
```

##### session(options)

1.Create a session middleware with the given options.  
 
**使用给定的选项创建一个会话中间件**

2.==Note== Session data is not saved in the cookie itself, just the session ID. Session data is stored server-side.
 
**注意:会话数据不是保存在他自己的cookie当中,cookie当中仅有一个session ID,会话数据是存储于服务端.**
 
3.==Note== Since version 1.5.0, the cookie-parser middleware no longer needs to be used for this module to work. This module now directly reads and writes cookies on req/res. Using cookie-parser may result in issues if the secret is not the same between this module and cookie-parser.
 
**注意:自版本1.5.0以后,这个模块在使用的使用不再需要使用cookie-parser中间件。现在这个模块直接在req/res的时候读取和写入cookie。如果当前模块和cookie-parser之间的加密是不一样的,使用cookie-parser可能导致问题.**

4.==Warning== The default server-side session storage, MemoryStore, is purposely not designed for a production environment. It will leak memory under most conditions, does not scale past a single process, and is meant for debugging and developing.
 
**警告:默认服务器端会话存储,内存存储,故意不用于生产环境。在大多数情况下它会泄漏内存,不存在缩小部分在一个单线程,用于调试和开发。**

5.For a list of stores, see compatible session stores.
 
**关于这个存储的列表,请参阅会话存储兼容.**
 
Options
express-session accepts these properties in the options object.
 
**express-session接受这些属性的选择对象。**

##### **cookie**
Settings object for the session ID cookie. The default value is { path: '/', httpOnly: true, secure: false, maxAge: null }.
 
**设置对象的cookie会话ID 。默认值为{路径:'/',httpOnly:true,secure:false,maxAge:null}。**

The following are options that can be set in this object.
 
**以下是选项,可以设置在这个对象中。**

###### cookie.domain
Specifies the value for the Domain Set-Cookie attribute. By default, no domain is set, and most clients will consider the cookie to apply to only the current domain.
 
**指定域SetCookkie属性的值.默认情况下,没有域.绝大多数的客户端都会考虑把cookie适用于当前域.**

###### cookie.expires
Specifies the Date object to be the value for the Expires Set-Cookie attribute. By default, no expiration is set, and most clients will consider this a "non-persistent cookie" and will delete it on a condition like exiting a web browser application.
 
**指定cookie的有效期,默认情况下,该值为空,绝大多数的客户端都考虑'非持久cookie',并且会通过删除这个cooke来完成退出登录的操作.**

==Note== If both expires and maxAge are set in the options, then the last one defined in the object is what is used.
 
**如果有效期和最大有效市场都设置,则只有最后一个定义的属性生效**

==Note== The expires option should not be set directly; instead only use the maxAge option.
 
**到期选项不应该直接设置;而不是只使用maxAge选项。**

cookie.httpOnly
Specifies the boolean value for the HttpOnly Set-Cookie attribute. When truthy, the HttpOnly attribute is set, otherwise it is not. By default, the HttpOnly attribute is set.
 
**指定的布尔值HttpOnly set - cookie属性。为真,设置HttpOnly属性。默认情况下,HttpOnly属性设置。**

==Note== be careful when setting this to true, as compliant clients will not allow client-side JavaScript to see the cookie in document.cookie.

 **注意:设置为true时要小心,比如兼容的客户是否允许客户端JavaScript看到document.cookie **


cookie.maxAge
Specifies the number (in milliseconds) to use when calculating the Expires Set-Cookie attribute. This is done by taking the current server time and adding maxAge milliseconds to the value to calculate an Expires datetime. By default, no maximum age is set.
 
**指定一个数(以毫秒为单位)计算到期时使用set - cookie属性。这是通过将当前服务器时间和增加maxAge毫秒值来计算一个datetime到期。默认情况下,没有设置最大年龄。**

==Note== If both expires and maxAge are set in the options, then the last one defined in the object is what is used.
 
**如果有效期和最大有效市场都设置,则只有最后一个定义的属性生效**

cookie.path
Specifies the value for the Path Set-Cookie. By default, this is set to '/', which is the root path of the domain.
 
**为cook的指定路径set - cookie的值。默认情况下,这个设置为'/',这是当前域的根路径。**

cookie.sameSite
Specifies the boolean or string to be the value for the SameSite Set-Cookie attribute.

**指定的布尔或字符串的值SameSite set - cookie属性**。

true will set the SameSite attribute to Strict for strict same site enforcement.

**为真,会将SameSite属性为同一站点执行严格。**

false will not set the SameSite attribute.
'lax' will set the SameSite attribute to Lax for lax same site enforcement.

**错误不会设置SameSite属性。
“宽松”将SameSite属性为同一站点宽松执法松懈。**

'strict' will set the SameSite attribute to Strict for strict same site enforcement.

**“严格”将SameSite属性为同一站点严格执行严格的。**

More information about the different enforcement levels can be found in the specification https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1.1

**更多信息可以在不同的执法水平规范https://tools.ietf.org/html/draft-west-first-party-cookies-07 section-4.1.1**

==Note== This is an attribute that has not yet been fully standardized, and may change in the future. This also means many clients may ignore this attribute until they understand it.

**请注意这是一个属性,还没有完全标准化,并在未来可能会改变。这也意味着许多客户可以忽略该属性,直到他们理解它。**

cookie.secure
Specifies the boolean value for the Secure Set-Cookie attribute. When truthy, the Secure attribute is set, otherwise it is not. By default, the Secure attribute is not set.

**为安全set - cookie属性指定的布尔值。当真相,安全属性设置,否则不是。默认情况下,没有设置安全属性。**

Note be careful when setting this to true, as compliant clients will not send the cookie back to the server in the future if the browser does not have an HTTPS connection.

**注意小心当设置为true,兼容客户不会发送cookie回服务器在未来如果浏览器没有HTTPS连接。**

Please note that secure: true is a recommended option. However, it requires an https-enabled website, i.e., HTTPS is necessary for secure cookies. If secure is set, and you access your site over HTTP, the cookie will not be set. If you have your node.js behind a proxy and are using secure: true, you need to set "trust proxy" in express:

**请注意安全:真的是推荐的选项。然而,它需要一个https-enabled网站,即。,HTTPS安全cookie是必要的。如果设置了安全,你通过HTTP访问你的网站,饼干不会设置。如果你的节点。js在代理和使用安全:真的,您需要设置“信任代理”在表达:**


```
var app = express()
app.set('trust proxy', 1) // trust first proxy 
app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}))
For using secure cookies in production, but allowing for testing in development, the following is an example of enabling this setup based on NODE_ENV in express:

var app = express()
var sess = {
  secret: 'keyboard cat',
  cookie: {}
}
 
if (app.get('env') === 'production') {
  app.set('trust proxy', 1) // trust first proxy 
  sess.cookie.secure = true // serve secure cookies 
}
 
app.use(session(sess))
```

The cookie.secure option can also be set to the special value 'auto' to have this setting automatically match the determined security of the connection. Be careful when using this setting if the site is available both as HTTP and HTTPS, as once the cookie is set on HTTPS, it will no longer be visible over HTTP. This is useful when the Express "trust proxy" setting is properly setup to simplify development vs production configuration.

**饼干。安全选项也可以被设置为一个特殊的值“汽车”这个设置自动匹配确定安全的连接。小心使用此设置时如果网站有两个HTTP和HTTPS,一旦饼干在HTTPS,它通过HTTP将不再可见。这是有用的表达“信任代理”设置时正确地设置来简化开发和生产配置。**

genid
Function to call to generate a new session ID. Provide a function that returns a string that will be used as a session ID. The function is given req as the first argument if you want to use some value attached to req when generating the ID.

**函数调用生成一个新的会话ID。提供一个函数,它返回一个字符串,该字符串将被用作一个会话ID。要求给出的函数是作为第一个参数,如果你想使用一些值附加到请求时生成的ID。**

The default value is a function which uses the uid-safe library to generate IDs.

**默认值是一个函数,使用uid-safe库生成id。**

NOTE be careful to generate unique IDs so your sessions do not conflict.

**注意小心生成惟一的id,以便您的会话不冲突。**


```
app.use(session({
  genid: function(req) {
    return genuuid() // use UUIDs for session IDs 
  },
  secret: 'keyboard cat'
}))
```

name
The name of the session ID cookie to set in the response (and read from in the request).

**会话ID cookie的名称设置在响应(以及从请求中读取)。**

The default value is 'connect.sid'.

**默认值是“connect.sid”。**

Note if you have multiple apps running on the same hostname (this is just the name, i.e. localhost or 127.0.0.1; different schemes and ports do not name a different hostname), then you need to separate the session cookies from each other. The simplest method is to simply set different names per app.

**注意如果您有多个应用程序运行在同一主机名(这只是一个名字,即localhost或127.0.0.1;不同的方案和港口不名称不同的主机名),那么您需要互相独立的会话cookie。最简单的方法是为每个应用程序简单地设置不同的名称。**

proxy
Trust the reverse proxy when setting secure cookies (via the "X-Forwarded-Proto" header).

**信任时,反向代理设置安全cookie(通过“X-Forwarded-Proto”头)。**

The default value is undefined.

**默认值是未定义的。**


true The "X-Forwarded-Proto" header will be used.
false All headers are ignored and the connection is considered secure only if there is a direct TLS/SSL connection.

**真正的“X-Forwarded-Proto”将使用标题。
假头被忽略和连接被认为是安全的只有直接TLS / SSL连接。**

undefined Uses the "trust proxy" setting from express

**未定义的使用表达的“信任代理”设置**

resave
Forces the session to be saved back to the session store, even if the session was never modified during the request. Depending on your store this may be necessary, but it can also create race conditions where a client makes two parallel requests to your server and changes made to the session in one request may get overwritten when the other request ends, even if it made no changes (this behavior also depends on what store you're using).

**部队会话保存会话存储,即使会话期间从来没有修改请求。取决于你的商店这可能是必要的,但它也可以创建竞态条件,客户让两个并行请求您的服务器,在一个请求中更改会话可能会覆盖另一个请求结束时,即使它没有改变(这种行为也取决于存储你使用)。**

The default value is true, but using the default has been deprecated, as the default will change in the future. Please research into this setting and choose what is appropriate to your use-case. Typically, you'll want false.

**默认值是正确的,但使用默认已经弃用,作为默认在未来将会改变。请研究这个设置,选择适合您的用例。通常情况下,你需要的是假的。**

How do I know if this is necessary for my store? The best way to know is to check with your store if it implements the touch method. If it does, then you can safely set resave: false. If it does not implement the touch method and your store sets an expiration date on stored sessions, then you likely need resave: true.

**我怎么知道这是必要的,为我的商店?知道最好的办法是检查与你的商店如果它实现了联系方法。如果是这样,那么您可以安全地重新保存:假的。如果它没有实现触摸的方法和你的商店设置过期日期存储会话,那么你可能需要重新保存:真的。**

rolling
Force a session identifier cookie to be set on every response. The expiration is reset to the original maxAge, resetting the expiration countdown.

**迫使cookie会话标识符被设置在每一个响应。重置到原始maxAge到期,到期重新设置倒计时。**

The default value is false.

**默认值是错误的。**

Note When this option is set to true but the saveUninitialized option is set to false, the cookie will not be set on a response with an uninitialized session.

**注意此选项设置为true时但saveUninitialized选项设置为false,饼干不会响应与未初始化会话。**

saveUninitialized
Forces a session that is "uninitialized" to be saved to the store. A session is uninitialized when it is new but not modified. Choosing false is useful for implementing login sessions, reducing server storage usage, or complying with laws that require permission before setting a cookie. Choosing false will also help with race conditions where a client makes multiple parallel requests without a session.

**部队一个会话是“未初始化”保存到存储。一个会话是未初始化的时候是新的但不修改。选择错误的是有用的实现登录会话,减少服务器存储使用,或遵守法律,要求许可之前设置一个cookie。选择错误与竞态条件,客户也将有助于使没有会话的多个并行请求。**

The default value is true, but using the default has been deprecated, as the default will change in the future. Please research into this setting and choose what is appropriate to your use-case.

**默认值是正确的,但使用默认已经弃用,作为默认在未来将会改变。请研究这个设置,选择适合您的用例。**

Note if you are using Session in conjunction with PassportJS, Passport will add an empty Passport object to the session for use after a user is authenticated, which will be treated as a modification to the session, causing it to be saved. This has been fixed in PassportJS 0.3.0

**注意如果您使用会话与PassportJS,护照将一个空的护照对象添加到会话用于用户身份验证后,将被视为修改会话,导致它被保存。这是固定在PassportJS 0.3.0**

secret
Required option

This is the secret used to sign the session ID cookie. This can be either a string for a single secret, or an array of multiple secrets. If an array of secrets is provided, only the first element will be used to sign the session ID cookie, while all the elements will be considered when verifying the signature in requests.

**这是秘密签署使用会话ID cookie。这可以是一个字符串为一个秘密,或多个秘密的数组。如果提供的秘密是一个数组,只有第一个元素将用于签署会话ID cookie,而所有元素将被认为是在验证签名的请求。**

store
The session store instance, defaults to a new MemoryStore instance.

**会话存储实例,默认为一个新的MemoryStore实例。**

unset
Control the result of unsetting req.session (through delete, setting to null, etc.).

**需要控制的结果进行调用。会话(通过删除、设置为null,等等)。**

The default value is 'keep'.

**默认值是“保持”。**

'destroy' The session will be destroyed (deleted) when the response ends.

**“摧毁”会话将被摧毁的反应结束的时候(删除)。**

'keep' The session in the store will be kept, but modifications made during the request are ignored and not saved.

**“保持”会话将一直在店里,但是修改请求被忽略和未得救。**

req.session
To store or access session data, simply use the request property req.session, which is (generally) serialized as JSON by the store, so nested objects are typically fine. For example below is a user-specific view counter:

**存储或访问会话数据,只需使用请求属性要求。会话,(通常)存储序列化为JSON,因此嵌套对象通常很好。例如下面是一个特定于用户的观点反驳:**


```
// Use the session middleware 
app.use(session({ secret: 'keyboard cat', cookie: { maxAge: 60000 }}))
 
// Access the session as req.session 
app.get('/', function(req, res, next) {
  var sess = req.session
  if (sess.views) {
    sess.views++
    res.setHeader('Content-Type', 'text/html')
    res.write('<p>views: ' + sess.views + '</p>')
    res.write('<p>expires in: ' + (sess.cookie.maxAge / 1000) + 's</p>')
    res.end()
  } else {
    sess.views = 1
    res.end('welcome to the session demo. refresh!')
  }
})
```

Session.regenerate(callback)
To regenerate the session simply invoke the method. Once complete, a new SID and Session instance will be initialized at req.session and the callback will be invoked.

**重新生成会话简单地调用该方法。一旦完成,一个新的SID,在点播会话实例将被初始化。会话和要调用的回调。**


```
req.session.regenerate(function(err) {
  // will have a new session here 
})
```

Session.destroy(callback)
Destroys the session and will unset the req.session property. Once complete, the callback will be invoked.

**破坏会话并将设置要求。会话属性。一旦完成,将调用回调。**


```
req.session.destroy(function(err) {
  // cannot access session here 
})
```

Session.reload(callback)
Reloads the session data from the store and re-populates the req.session object. Once complete, the callback will be invoked.

**重新加载的会话数据存储和重新填充点播。会话对象。一旦完成,将调用回调。**


```
req.session.reload(function(err) {
  // session updated 
})
```

Session.save(callback)
Save the session back to the store, replacing the contents on the store with the contents in memory (though a store may do something else--consult the store's documentation for exact behavior).

**保存会话回商店,替换内容与内容存储在内存中(尽管商店可能做其他的事情——咨询具体行为)的存储的文档。**

This method is automatically called at the end of the HTTP response if the session data has been altered (though this behavior can be altered with various options in the middleware constructor). Because of this, typically this method does not need to be called.

**调用这个方法是自动的HTTP响应如果会话数据已经改变了(尽管这种行为可以改变各种选项的中间件构造函数)。因此,通常不需要调用这个方法。**

There are some cases where it is useful to call this method, for example, long- lived requests or in WebSockets.

**有一些情况下,调用这个方法是很有用的,例如,长期居住或WebSockets请求。**


```
req.session.save(function(err) {
  // session saved 
})
```

Session.touch()
Updates the .maxAge property. Typically this is not necessary to call, as the session middleware does this for you.

**更新。maxAge财产。通常这没有必要调用,因为会话中间件这是否适合你。**

req.session.id
Each session has a unique ID associated with it. This property will contain the session ID and cannot be modified.

**每个会话都有一个与之关联的惟一ID。这个属性将包含会话ID,不能修改。**

req.session.cookie
Each session has a unique cookie object accompany it. This allows you to alter the session cookie per visitor. For example we can set req.session.cookie.expires to false to enable the cookie to remain for only the duration of the user-agent.

**每个会话都有一个独特的cookie对象陪它。这允许您更改每个访问者的会话cookie。例如,我们可以设置req.session.cookie。到期为false,使饼干保持用户代理的持续时间。**

Cookie.maxAge
Alternatively req.session.cookie.maxAge will return the time remaining in milliseconds, which we may also re-assign a new value to adjust the .expires property appropriately. The following are essentially equivalent

var hour = 3600000
req.session.cookie.expires = new Date(Date.now() + hour)
req.session.cookie.maxAge = hour
For example when maxAge is set to 60000 (one minute), and 30 seconds has elapsed it will return 30000 until the current request has completed, at which time req.session.touch() is called to reset req.session.maxAge to its original value.

req.session.cookie.maxAge // => 30000 
req.sessionID
To get the ID of the loaded session, access the request property req.sessionID. This is simply a read-only value set when a session is loaded/created.

Session Store Implementation

Every session store must be an EventEmitter and implement specific methods. The following methods are the list of required, recommended, and optional.

Required methods are ones that this module will always call on the store.
Recommended methods are ones that this module will call on the store if available.
Optional methods are ones this module does not call at all, but helps present uniform stores to users.
For an example implementation view the connect-redis repo.

store.all(callback)
Optional

This optional method is used to get all sessions in the store as an array. The callback should be called as callback(error, sessions).

store.destroy(sid, callback)
Required

This required method is used to destroy/delete a session from the store given a session ID (sid). The callback should be called as callback(error) once the session is destroyed.

store.clear(callback)
Optional

This optional method is used to delete all sessions from the store. The callback should be called as callback(error) once the store is cleared.

store.length(callback)
Optional

This optional method is used to get the count of all sessions in the store. The callback should be called as callback(error, len).

store.get(sid, callback)
Required

This required method is used to get a session from the store given a session ID (sid). The callback should be called as callback(error, session).

The session argument should be a session if found, otherwise null or undefined if the session was not found (and there was no error). A special case is made when error.code === 'ENOENT' to act like callback(null, null).

store.set(sid, session, callback)
Required

This required method is used to upsert a session into the store given a session ID (sid) and session (session) object. The callback should be called as callback(error) once the session has been set in the store.

store.touch(sid, session, callback)
Recommended

This recommended method is used to "touch" a given session given a session ID (sid) and session (session) object. The callback should be called as callback(error) once the session has been touched.

This is primarily used when the store will automatically delete idle sessions and this method is used to signal to the store the given session is active, potentially resetting the idle timer.

Compatible Session Stores

The following modules implement a session store that is compatible with this module. Please make a PR to add additional modules :)

★ aerospike-session-store A session store using Aerospike.

★ cassandra-store An Apache Cassandra-based session store.

★ cluster-store A wrapper for using in-process / embedded stores - such as SQLite (via knex), leveldb, files, or memory - with node cluster (desirable for Raspberry Pi 2 and other multi-core embedded devices).

★ connect-azuretables An Azure Table Storage-based session store.

★ connect-cloudant-store An IBM Cloudant-based session store.

★ connect-couchbase A couchbase-based session store.

★ connect-datacache An IBM Bluemix Data Cache-based session store.

★ connect-db2 An IBM DB2-based session store built using ibm_db module.

★ connect-dynamodb A DynamoDB-based session store.

★ connect-loki A Loki.js-based session store.

★ connect-ml A MarkLogic Server-based session store.

★ connect-mssql A SQL Server-based session store.

★ connect-monetdb A MonetDB-based session store.

★ connect-mongo A MongoDB-based session store.

★ connect-mongodb-session Lightweight MongoDB-based session store built and maintained by MongoDB.

★ connect-pg-simple A PostgreSQL-based session store.

★ connect-redis A Redis-based session store.

★ connect-memcached A memcached-based session store.

★ connect-session-knex A session store using Knex.js, which is a SQL query builder for PostgreSQL, MySQL, MariaDB, SQLite3, and Oracle.

★ connect-session-sequelize A session store using Sequelize.js, which is a Node.js / io.js ORM for PostgreSQL, MySQL, SQLite and MSSQL.

★ express-mysql-session A session store using native MySQL via the node-mysql module.

★ express-oracle-session A session store using native oracle via the node-oracledb module.

★ express-sessions: A session store supporting both MongoDB and Redis.

★ connect-sqlite3 A SQLite3 session store modeled after the TJ's connect-redis store.

★ documentdb-session A session store for Microsoft Azure's DocumentDB NoSQL database service.

★ express-nedb-session A NeDB-based session store.

★ express-session-level A LevelDB based session store.

★ express-etcd An etcd based session store.

★ fortune-session A Fortune.js based session store. Supports all backends supported by Fortune (MongoDB, Redis, Postgres, NeDB).

★ hazelcast-store A Hazelcast-based session store built on the Hazelcast Node Client.

★ level-session-store A LevelDB-based session store.

★ medea-session-store A Medea-based session store.

★ mssql-session-store A SQL Server-based session store.

★ nedb-session-store An alternate NeDB-based (either in-memory or file-persisted) session store.

★ sequelstore-connect A session store using Sequelize.js.

★ session-file-store A file system-based session store.

★ session-rethinkdb A RethinkDB-based session store.

Example

A simple example using express-session to store page views for a user.

var express = require('express')
var parseurl = require('parseurl')
var session = require('express-session')
 
var app = express()
 
app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true
}))
 
app.use(function (req, res, next) {
  var views = req.session.views
 
  if (!views) {
    views = req.session.views = {}
  }
 
  // get the url pathname 
  var pathname = parseurl(req).pathname
 
  // count the views 
  views[pathname] = (views[pathname] || 0) + 1
 
  next()
})
 
app.get('/foo', function (req, res, next) {
  res.send('you viewed this page ' + req.session.views['/foo'] + ' times')
})
 
app.get('/bar', function (req, res, next) {
  res.send('you viewed this page ' + req.session.views['/bar'] + ' times')
})
License

MIT

We ♥ your boss
Selectively mirror the npm registry inside your firewall. Filter packages based on security, licensing, code quality and more. Build awesome stuff faster. Try npm Enterprise for free…


npm install express-session
how? learn more

 dougwilson dougwilson published 4 weeks ago
1.15.2 is the latest of 52 releases
github.com/expressjs/session
MIT  Licensed on OSI-approved terms®
Collaborators list
defunctzombie
dougwilson
mscdex
Stats
80,221 downloads in the last day
446,223 downloads in the last week
1,894,335 downloads in the last month
34 open issues on GitHub
17 open pull requests on GitHub
Try it out
Test express-session in your browser.
Keywords
None

Dependencies (9)
cookie, cookie-signature, crc, debug, depd, on-headers, parseurl, uid-safe, utils-merge

Dependents (1576)
betspots, sdk-snips-ai, fx-middleware, jxappsrvr, ngnode, goose-session, roadiejs-api, pk-app-webgui-aria2, zetta-app, snx-middleware, clever-auth, maki-passport-local, scio, powerstone, azquestion.com, pk-app-fbgui-aria2, omni.cm, generaljs, taller-abm, radiatus-providers, number_game, irc-bnc, sycle-gateway, tome, express-boobst, noful, saber-storage, crud-middleware, m2m-supervisor, nopar, baucis-decorators-example, wxchangba, makingmobile, elastic-transfer, sublime-application, neyka, reacta-service-express, nimbleservice, super-bootstrap, mockcenter, latentflip-vorlon, tumojs, timetracker, powerjs, nodeplayer-plugin-passport, super-server, pe-n-starter, nej-webserver, weather-forecast-application, pump.io-client-app, and more

Voxer is hiring. View more…
You Need Help

Documentation
Support / Contact Us
Registry Status
Website Issues
CLI Issues
Security
About npm

About npm, Inc
Jobs
npm Weekly
Blog
Twitter
GitHub
Legal Stuff

Terms of Use
Code of Conduct
Package Name Disputes
Privacy Policy
Reporting Abuse
Other policies
npm loves you
