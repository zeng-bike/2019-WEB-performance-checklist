```
    原文链接地址：https://www.smashingmagazine.com/2019/01/front-end-performance-checklist-2019-pdf-pages/
    本文译自维塔利弗里德曼的前端性能优化清单的文章--2019篇幅。
    这是一篇有关年度前端性能检查的文章，包含了创建快速体验所需的所有知识，自2016年以来每年更新一次。
```

## 目录
* 规划和指标
* 设定现实目标
* 定义环境
* 构建优化
* 资源优化
* 交互优化
* HTTP / 2
* 测试和监测
* 快速取胜

#### 规划和指标
1. **建立性能文化**

    只要没有业务支撑，公司的业绩就不会长期持续。 进入客户服务部门研究常见的投诉，看看如何提高业绩并且
帮助缓解这些问题。建立一个公司定制的案例研究与实际数据和业务指标。在设计过程中计划加载顺序和权衡。

2. **比你最快的竞争对手快20％**

    在代表受众的设备上收集数据。比起模拟，更喜欢真实的设备。选择一款 Moto G4 ，一款三星的中档手机，一款像 
Nexus 5X 这样的中档手机和速度较慢的设备，比如 Alcatel 1X 或 Nexus 2 。另外，模拟移动设备通过测试一个节流网络（例如： 150ms RTT, 1.5 Mbps down, 0.7 Mbps up ）压制CPU（5倍放缓的速度 ）。然后切换到普通的3G、4G和Wi-Fi。收集数据，建立电子表格，削减20%，制定目标(性能预算)。

3. **选择正确的指标**

    并非每一个指标都同等重要。研究什么指标最重要：通常是**最重要**的关系到你可以多快开始**渲染最重要的像素**和多快你可以**提供输入的响应能力**。根据客户的感知，优先考虑 **页面加载、时间交互、第一次输入延迟、英雄渲染时间、第一次有意义的绘制、速度指标**，通常这些指标都很重要。

4. **设置 `clear` 和 `customer` 配置文件以进行测试**

    关闭杀毒和后台CPU任务，删除后台带宽传输和使用不带浏览器扩展的干净用户配置文件进行测试，以避免不正确的结果。研究客户使用的扩展，并使用专用的 **客户** 配置文件进行测试。

5. **与同事分享清单**

    确保团队中的每个成员都熟悉这份清单。每一个决定都会影响性能，项目将从积极参与的前端开发人员那里获得巨大的好处。根据性能预算制定来设计决策。

#### 设定现实目标

1. **响应时间控制在 100ms，帧速控制在 60帧/秒**

    每一帧动画的完成时间应该少于 16ms — 理想情况下是 10ms ,从而实现 60帧/秒 ( 1秒 ÷ 60 = 16.6ms )。
    #### 保持乐观和明智地利用空闲时间。对于像动画这样的高压点，最好这样做没有什么是你能做到的，也没有什么是你不能做到的。估计输入延迟应该小于50ms。明智地利用空闲时间，用空闲的时间等待紧急的来临。

2. **速度指标（SpeedIndex） < 1250，3G上的交互时间（Interaction time）小于5s**

    我们的目标是一次有效的渲染控制在1秒内(在快速连接上)并且保证速度指标值小于 1250ms 。考虑到我们的最好条件是一个200美元的Android手机在一个缓慢的3G的环境下，模拟 400ms [RTT](https://baike.baidu.com/item/RTT/4746617?fr=aladdin) 和 400kb 传输速度下进行仿真，我们的目标是交互时间控制在 **小于5s**，并且保证 2 - 3s 内再次访问。

3. **关键有效负载块= 14KB，关键文件大小预算<170KB**

    **HTML** 的前 14KB 是 **最关键的有效负载块** -- 并且是第一次往返中可以提供的预算的唯一部分（由于移动唤醒时间，这是在400ms [RTT](https://baike.baidu.com/item/RTT/4746617?fr=aladdin) 下1秒内获得的）。
    另一方面，由于 `JavaScript` 解析时间的原因，我们对内存和CPU 有硬件限制。为了实现第一段中所述的目标，我们必须考虑 `JavaScript` 的关键文件大小预算。关于预算应该是多少的意见（并且它在很大程度上取决于你的项目的性质），但是预算为 170KB 的JavaScript 压缩包已经需要花费 1s 才能在普通手机上进行解析和编译。假设在解压缩（0.7MB）时 170KB 扩展到3倍大小，那已经可能是 Moto G4 或 Nexus 2 上体现用户体验的丧钟。性能预算可能不应该是固定值。根据网络连接，性能预算应该适应，但慢速连接​​上的负载更加昂贵，无论它们如何使用。

#### 定义环境

1. **选择并设置构建工具**

    不要太注意所谓的酷。只要你快速得到结果，你没有问题维护你的构建过程，你就已经做得很好。 唯一的例外可能是 `Webpack` ，它提供了许多有用的优化技术。 如果它还没有使用，请务必仔细查看 `code-splitting`**(代码分割)** 和 `tree-shaking`**(摇树优化)**。

2. **使用渐进增强作为默认值**

    首先设计和构建核心体验，然后通过功能强大的浏览器的高级功能增强体验，创建弹性体验。如果您的网站在次优网络上的浏览器中屏幕较差的慢速计算机上运行速度很快，那么它在具有良好浏览器的快速计算机上运行得更快。

3. **选择强大的性能基准**

    JavaScript的体验成本最高。 由于 170KB 的预算已包含关键路径 `HTML` / `CSS` / `JavaScript`，路由器，状态管理，实用程序，框架和应用程序逻辑，我们必须彻底检查网络传输成本，解析/编译时间和运行时成本。

4. **评估每个框架和每个依赖项**

    现在，并非每个项目都需要一个框架，并且单页应用程序的每个页面都不需要加载框架。JS 框架慎重选择。在选择一个框架前：先评估第三方JS的特性，可访问性，稳定性，性能，包生态系统，社区，学习曲线，文档，工具，跟踪记录，团队，兼容性和安全性。例如：`ReactJs`， `Preact CLI`，和 `PWA StarterKit` 为一般移动硬件提供了合理的默认快速加载。

5. **明智地选择你的战斗武器：`React` ，`Vue` ，`Angular`，`Ember` 和 `Co`**

    不同的框架会对性能产生不同的影响，并且需要不同的优化策略，因此您必须清楚地了解您将依赖的框架的所有细节。构建Web应用程序时，请查看 [PRPL模式](https://developers.google.com/web/fundamentals/performance/prpl-pattern/) 和 [应用程shell体系结构](https://developers.google.com/web/updates/2015/11/app-shell)。这个想法非常简单：推送初始路由的交互所需的最小代码，以便快速呈现，然后使用服务工作者进行缓存和预缓存资源，然后异步地延迟加载所需的路由。

6. **优化 API 的性能**

    如果许多资源需要来自 API 的数据， API 可能会成为性能瓶颈。
考虑使用 [GraphQL](https://graphql.org/) ，一种查询语言和一个服务器端运行时来执行查询
使用您为数据定义的类型系统。 与 [REST](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/) 不同，[GraphQL](https://graphql.org/) 可以检索一个中的所有数据
单个请求，没有过多或欠读取数据，因为它通常发生在 [REST](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)  中。

7. **你会使用 AMP 或 Instant Articles 吗**

    根据您组织的优先级和策略，您可能需要考虑使用 Google 的 [AMP](https://www.ampproject.org/) 或 Facebook 的 [Instant Articles](https://instantarticles.fb.com/) 或 Apple 的 [Apple News](https://www.apple.com/news/) 。如果没有它们，您可以获得良好的性能，但 [AMP](https://www.ampproject.org/) 确实提供了一个可靠的性能框架和免费的内容交付网络 CDN ，而 [Instant Articles](https://instantarticles.fb.com/) 将提高您在Facebook上的可见性和性能。

8. **明智地选择你的 CDN**

    根据您拥有的动态数据量，您可以将内容的某些部分 **外包** 到  [静态站点生成器](https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/) ，将其推送到 CDN 并从中提供静态版本，从而避免数据库请求。您甚至可以选择基于 CDN 的 [静态托管平台](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/) ，通过交互式组件丰富您的页面作为增强功能 [JAMStack](https://jamstack.org/) 。实际上，其中一些生成器（比如 **React** 之上的 [Gatsby](https://www.gatsbyjs.org/blog/2017-09-13-why-is-gatsby-so-fast/) ）实际上是 [网站编译器](https://tomdale.net/2017/09/compilers-are-the-new-frameworks/) ，提供了许多开箱即用的自动优化。随着编译器随着时间的推移添加优化，编译后的输出随着时间的推移变得越来越小。

#### 构建优化

1. **确定您的优先事项**

    首先最好明确的知道您在处理什么。运行所有资产的清单( `JavaScript `、图像、字体、第三方脚本、页面上的 **昂贵** 模块)，并将它们分组。定义旧版浏览器的基本核心体验（即完全可访问的核心内容），功能强大的浏览器的增强体验（即丰富的完整体验）和附加功能（不是绝对需要且可以延迟加载的资产，例如网页字体，不必要的样式，轮播脚本，视频播放器，社交媒体按钮，大图像）。不久前，我们发表了一篇关于 [改进粉碎杂志的表现](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/) 的文章，详细描述了这种方法。

2. **重新审视好的 切割芥末（`cutting-the-mustard`） 技术**

    如今，我们仍然可以使用 [切割技术](https://www.filamentgroup.com/lab/modernizing-delivery.html) 将核心体验发送到传统浏览器，并为现代浏览器提供增强的体验。该 [技术](https://snugug.com/musings/modern-cutting-the-mustard/) 的 [更新变体](https://snugug.com/musings/modern-cutting-the-mustard/) 将使用 `ES2015+ <script type="module">`。现代浏览器会将脚本解释为 `JavaScript` 模块并按预期运行它，而旧版浏览器无法识别该属性并忽略它，因为它是未知的 `HTML` 语法。一些廉价 Android 手机主要运行 Chrome 浏览器，尽管内存和CPU功能有限，但仍将 **削减芥末** 。最终，使用 [设备内存客户端提示标题](https://github.com/w3c/device-memory) ，我们将能够更可靠地定位低端设备。在编写本文时，仅在 Blink 中支持标头（通常用于 [客户端提示](https://caniuse.com/#search=client%20hints) ）。由于设备内存还有一个 [已在 Chrome 浏览器中提供](https://developers.google.com/web/updates/2017/12/device-memory) 的 `JavaScript API`  ，因此一种选择可能是基于 `API` 进行检测，并且只有在不支持时才会回归 **切割芥末** 技术

3. **解析 `JavaScript` 是昂贵的，所以保持小**

    在处理单页面应用程序 **SPA** 时，我们需要一些时间来初始化应用程序，然后才能呈现页面。您的设置将需要您的自定义解决方案，但您可以留意模块和技术，以加快初始渲染时间（在低端移动设备上，[解析和执行时间很容易高出2-5倍](https://medium.com/reloading/javascript-start-up-performance-69200f43b201) ）。

4. **使用 树形抖动（`Tree-shaking`） ，作用域提升（`Scope hoisting`）和代码分割（`Code-splitting`）来减少有效负载**

    [树形抖动](https://developers.google.com/web/fundamentals/performance/optimizing-javascript/tree-shaking/) 是一种清理构建过程的方法，通过仅包含实际用于生产的代码并消除 [Webpack](http://2ality.com/2015/12/webpack-tree-shaking.html) 中未使用的导入。通过 Webpack 和 Rollup ，我们还提供了[范围提升](https://medium.com/webpack/brief-introduction-to-scope-hoisting-in-webpack-8435084c171f)，允许两个工具检测链接可以展平的位置，并转换为一个内联函数，而不会影响代码。通过 WebPack 使用他们。 [代码拆分](https://webpack.js.org/guides/code-splitting/) 是另一个Webpack功能，它将您的代码库拆分为按需加载的 **块**。

5. **能否将 JavaScript 卸载到 Web Worker 中**

    随着代码库的不断增长，UI性能瓶颈将会出现，从而降低用户的体验。那是因为 [DOM操作](https://medium.com/google-developer-experts/running-fetch-in-a-web-worker-700dc33ac854) 与主线程上的 [JavaScript一起运行](https://medium.com/google-developer-experts/running-fetch-in-a-web-worker-700dc33ac854)。对于 [Web worker](https://flaviocopes.com/web-workers/)，我们可以将这些昂贵的操作移动到在不同线程上运行的后台进程。Web工作者的典型用例是 [预取数据和Progressive Web Apps](https://blog.sessionstack.com/how-javascript-works-the-building-blocks-of-web-workers-5-cases-when-you-should-use-them-a547c0757f6a) 以提前加载和存储一些数据，以便您以后可以在需要时使用它。可以考虑编译成
[WebAssembly](https://webassembly.org/) 这个最适合计算密集型 Web 应用程序。

6. **差异化服务**

    由于 ES2015 在 [现代浏览器](http://kangax.github.io/compat-table/es6/) 中得到了  [非常好的支持](http://kangax.github.io/compat-table/es6/)，我们可以使用 [babel-preset-env](http://2ality.com/2017/02/babel-preset-env.html) 仅转换您所针对的现代浏览器不支持的ES2015 +功能。然后设置 [两个构建](https://gist.github.com/newyankeecodeshop/79f3e1348a09583faf62ed55b58d09d9)，一个在ES6中，一个在ES5中。如上所述，现在所有 [主流浏览器](https://caniuse.com/#feat=es6-module) 都 [支持](https://caniuse.com/#feat=es6-module) JavaScript 模块，因此使用 [usescript type="module"](https://developers.google.com/web/fundamentals/primers/modules) 来让支持ES模块的浏览器加载文件，而旧浏览器可以加载旧版本 `Script nomodule`。我们可以使用 [Webpack ESNext Boilerplate](https://github.com/philipwalton/webpack-esnext-boilerplate) 自动完成整个过程。对于lodash，使用 [babel-plugin-lodash](https://github.com/lodash/babel-plugin-lodash) 它将仅加载您在源中使用的模块。您的依赖项也可能依赖于其他版本的Lodash，因此 [将通用lodash requires转换为挑选的lodash](https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/) 以避免代码重复。这可能会为您节省相当多的 JavaScript 负载。

7. **通过增量解耦识别和重写遗留代码**

    长寿项目倾向于收集灰尘和过时的代码。重新访问您的依赖项并评估重构或重写最近导致问题的遗留代码所需的时间。当然，它始终是一项重大任务，但是一旦您了解遗留代码的影响，就可以从 [增量解耦](https://githubengineering.com/removing-jquery-from-github-frontend/) 开始。首先，设置指标，跟踪遗留代码调用的比率是保持不变还是下降，而不是上升。公开阻止团队使用该库，并确保您的 CI [警告](https://github.com/dgraham/eslint-plugin-jquery) 开发人员，如果它在拉取请求中使用。[polyfills](https://githubengineering.com/removing-jquery-from-github-frontend/#polyfills) 可以帮助从遗留代码转换为使用标准浏览器功能的重写代码库。

8. **识别并删除未使用的 `CSS` / `JavaScript`**

    Chrome 浏览器中的 [CSS和JavaScript代码覆盖率](https://developers.google.com/web/updates/2017/04/devtools-release-notes#coverage) 允许您了解哪些代码已执行/已应用，哪些代码尚未执行。您可以开始记录覆盖范围，在页面上执行操作，然后浏览代码覆盖率结果。一旦检测到未使用的代码，[找到那些模块和延迟加载 `import()`](https://twitter.com/TheLarkInn/status/1012429019063578624)（参见整个线程）。然后重复覆盖配置文件并验证它现在在初始加载时发送的代码较少。您可以使用 [Puppeteer](https://github.com/GoogleChrome/puppeteer) 以编程方式收集代码覆盖率，Canary也允许您导出代码覆盖率结果。正如 Andy Davies 指出的那样，您可能希望收集现代和旧版浏览器的代码覆盖率。[Puppeteer](https://github.com/GoogleChrome/puppeteer) 还有许多 [其他用例](https://github.com/GoogleChromeLabs/puppeteer-examples)，例如：[自动视觉差异](https://meowni.ca/posts/2017-puppeteer-tests/) 或 [监视每个构建的未使用的CSS](http://blog.cowchimp.com/monitoring-unused-css-by-unleashing-the-devtools-protocol/)。

9.  **修剪 `JavaScript` 依赖项的大小**

    正如 Addy Osmani 指出的那样，当你只需要一个分数时，你很可能会发送完整的 JavaScript 库，以及不需要它们的浏览器的日期 [polyfill](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)，或者只是重复代码。为避免开销，请考虑使用 [webpack-libs-optimization](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)，在构建过程中删除未使用的方法和 [polyfill](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)。将捆绑审核添加到常规工作流程中。

10. **您是否正在使用 `JavaScript` 块的预测预取**

    我们可以使用启发式方法来决定何时预加载 JavaScript 块。[Guess.js](https://github.com/guess-js/guess) 是一组工具和库，它们使用 Google Analytics 数据来确定用户最有可能从给定页面访问哪个页面。但是需要注意的是:您可能会提示浏览器使用不需要的数据并预取不需要的页面，因此在预取请求的数量上保持相当保守是个好主意。一个好的用例是预取结帐中所需的验证脚本，或者当一个关键的号召性用语进入视口时的推测性预取。

11. **考虑微优化和 [渐进式启动](https://aerotwist.com/blog/when-everything-is-important-nothing-is/)**

    在这两种情况下，我们的目标应该是设置 [渐进式启动](https://aerotwist.com/blog/when-everything-is-important-nothing-is/)：使用服务器端渲染来获得快速的第一个有意义的绘制，但也包括一些最小的必要 JavaScript，以保持交互时间接近第一个有意义的绘制。如果 JavaScript 在 First Meaningful Paint 之后来得太晚，浏览器可能会在解析，编译和执行后期发现的 JavaScript 时[锁定主线程](https://davidea.st/articles/measuring-server-side-rendering-performance-is-tricky)，从而给 [站点或应用程序](https://philipwalton.com/articles/why-web-developers-need-to-care-about-interactivity/) 的[交互](https://philipwalton.com/articles/why-web-developers-need-to-care-about-interactivity/) 带来手铐。为了避免它，总是将函数的执行分解为单独的异步任务，并尽可能使用 `requestIdleCallback`。考虑使用 WebPack 的动态 `import()` 支持延迟加载 UI 部分，避免加载，解析和编译成本，直到用户真正需要它们。

12. **限制第三方脚本的影响**

    通过所有性能优化，我们通常无法控制来自业务需求的第三方脚本。这时候建议从自己的服务器，而不是从供应商的服务器加载第三方脚本。另一种选择是建立 **内容安全策略（CSP）** 以限制第三方脚本的影响，例如禁止下载音频或视频。最好的选择是通过嵌入脚本，`<iframe>` 以便脚本在 **iframe** 的上下文中运行，因此无法访问页面的 DOM ，也无法在您的域上运行任意代码。可以使用该 `sandbox` 属性进一步约束 `iframe` ，因此您可以禁用 `iframe` 可能执行的任何功能，例如阻止脚本运行，阻止警报，表单提交，插件，访问顶部导航等。如果要[对第三方进行压力测试](https://csswizardry.com/2017/07/performance-and-resilience-stress-testing-third-parties/)，请检查 DevTools 中性能配置文件页面中的自下而上的摘要，测试如果请求被阻止或超时的情况会发生什么 - 对于后者，您可以使用 WebPageTest 的 Blackhole 服务器 `blackhole.webpagetest.org` ，您可以将特定域指向在你的 `hosts` 文件中。

13. **正确设置 HTTP 缓存头**

    仔细检查 `expires`， `cache-control`， `max-age` 和其他 HTTP 缓存标头是否已正确设置。通常，资源应该可以在[非常短的时间内（如果它们可能更改）或无限期（如果它们是静态的）](https://jakearchibald.com/2016/caching-best-practices/) 可缓存- 您只需在需要时更改 URL 中的版本。禁用 `Last-Modified` 标头，因为任何带有它的资产都会导致带有 `If-Modified-Since-header` 的条件请求，即使资源位于缓存中也是如此。与 ... 相同 Etag 。使用 `Cache-control: immutable`，专为指纹静态资源设计，以避免重新验证（截至2018年12月，[Firefox，Edge和Safari支持](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) ；仅在 https:// 事务中支持 Firefox ）。事实上，在HTTP存档中的所有页面中， `2％` 的请求和 `30％` 的网站似乎 [包含至少1个不可变响应](https://discuss.httparchive.org/t/cache-control-immutable-a-year-later/1195)。另外，大多数使用它的网站都在具有长寿新生。而且需要注意的是，仔细检查你是不是发送不必要的报头（例如 `x-powered-by`， `pragma`， `x-ua-compatible`， `expires`和其他人）和你包括 [有用的安全和性能头](https://www.fastly.com/blog/headers-we-want) （如 `Content-Security-Policy`， `X-XSS-Protection`， `X-Content-Type-Options`等）。最后，请记住单页应用程序中 [CORS 请求](https://medium.com/@ankur_anand/the-terrible-performance-cost-of-cors-api-on-the-single-page-application-spa-6fcf71e50147) 的 [性能成本](https://medium.com/@ankur_anand/the-terrible-performance-cost-of-cors-api-on-the-single-page-application-spa-6fcf71e50147)。

#### 资源优化

1. **使用 [Brotli](https://github.com/google/brotli) 或 Zopfli 进行纯文本压缩**
    
    [Brotli](https://github.com/google/brotli) 是一种新的无损数据格式，现在所有现代浏览器都支持，它
比 Gzip 和 Deflate 更有效。压缩可能（非常）慢，具体取决于设置，但较慢的压缩最终会导致更高的压缩率。所以，我们的应对策略是：使用最高级别的 [Brotli + Gzip预压缩静态资产](https://css-tricks.com/brotli-static-compression/)，并使用 [Brotli](https://github.com/google/brotli) 在1-4级动态压缩（动态）HTML。确保服务器正确处理 [Brotli](https://github.com/google/brotli) 或gzip的内容协商。如果您无法在服务器上安装/维护 [Brotli](https://github.com/google/brotli)，请使用 [Brotli](https://github.com/google/brotli)。

2. **使用 [响应式图像](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/) 和 [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/)**

    尽可能使用 [响应式图像](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/) 与 `srcset` ， `sizes` 和 `<picture>` 元素。当然您也可以通过使用元素和 JPEG 后备（参见 Andreas Bovens 的 [代码片段](https://dev.opera.com/articles/responsive-images/#different-image-types-use-case)）或者通过提供 [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/) 图像来使用 [WebP格式](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/)（在 Chrome，Opera，Firefox 65，Edge 18 中支持）。使用内容协商（使用标头）。重要的是要注意，虽然WebP图像文件大小与 [等效的Guetzli和Zopfli相比](https://www.ctrl.blog/entry/webp-vs-guetzli-zopfli)，但格式 [不支持像JPEG](https://youtu.be/jTXhYj2aCDU?t=630) 这样的 [渐进式渲染](https://youtu.be/jTXhYj2aCDU?t=630)，这就是为什么用户可以通过良好的JPEG 更快地看到实际图像，尽管 [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/) 图像可能会更快通过网络。使用 JPEG ，我们可以使用半数甚至四分之一的数据提供 **体面** 的用户体验，然后加载其余数据，而不是像 [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/) 那样拥有半空图像。您的决定取决于您的目标：使用[WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/)，您将减少有效负载，使用 JPEG，您将提高感知性能。

3. **图像是否恰当优化**

    当您在着陆页上工作时，特定图像的加载速度非常快，请确保 JPEG 是渐进式的，并使用 [mozJPEG](https://github.com/mozilla/mozjpeg) 进行压缩（通过操纵扫描级别来改善开始渲染时间）或 [Guetzli](https://github.com/google/guetzli)，Google浏览器的新开放式源编码器专注于感知性能，并利用 Zopfli 和 WebP 的学习。[唯一的缺点是](https://medium.com/@fox/talk-the-state-of-the-web-3e12f8e413b3)：处理时间较慢（每百万像素CPU一分钟）。对于 PNG，我们可以使用 [Pingo](http://css-ig.net/pingo)，对于 SVG，我们可以使用 [SVGO](https://www.npmjs.com/package/svgo) 或 [SVGOMG](https://jakearchibald.github.io/svgomg/)。如果您需要从网站上快速预览，复制或下载所有SVG资产，请使用 [svg-grabber](https://chrome.google.com/webstore/detail/svg-grabber-get-all-the-s/ndakggdliegnegeclmfgodmgemdokdmg) 也能为你做到这一点。您使用 [Squoosh](https://squoosh.app/) 以最佳压缩级别（有损或无损）压缩，调整大小和操作图像。如果要检查响应式标记的效率，可以使用 [映像堆](https://github.com/filamentgroup/imaging-heap)，这是一种命令行工具，可以测量视口大小和设备像素比率的效率。
    
4. **视频是否已恰当优化**

    坦率地说，不是加载影响渲染性能和带宽的重型动画 GIF，而是切换到动画 WebP （GIF是后备）或者用 [循环HTML5视频](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/replace-animated-gifs-with-video/) 替换它们是个好主意。是的，浏览器性能很慢 `<video>`，并且与图像不同，浏览器不会预加载 `<video>` 内容，但它们往往比 GIF 更轻更小。不是一个选择？好吧，至少我们可以使用 [Lossy GIF](https://kornel.ski/lossygif)， [gifsicle](https://github.com/kohler/gifsicle) 或 [giflossy](https://github.com/kornelski/giflossy) 为 GIF 添加有损压缩。目前，最广泛使用和支持的编码是 H.264，由 MP4 文件提供服务，因此在提供文件之前，请确保使用 [多通道编码](https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77) 处理 MP4 ，并使用 [frei0r iirblur效果模糊](https://yalantis.com/blog/experiments-with-ffmpeg-filters-and-frei0r-plugin-effects/) （如果适用） [moov atom metadata](https://www.adobe.com/devnet/video/articles/mp4_movie_atom.html) 移动到文件头部，而服务器 [接受字节服务](https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77)。 `Boris Schapira` 为 [FFmpeg](https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77) 提供了 [最大限度优化视频的准确说明](https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77)。当然，提供WebM格式作为替代方案也会有所帮助。

5. **Web 字体已恰当优化**

    第一个值得询问的问题是，您是否可以首先使用 [UI系统字体](https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/)。如果不是这种情况，那么您所服务的网络字体可能包括字形以及未使用的额外功能和权重。您可以要求您的类型代工厂部署 Web 字体，或者如果您使用的是开源字体，请使用 [Glyphhanger](https://www.afasterweb.com/2018/03/09/subsetting-fonts-with-glyphhanger/) 或 [Fontsquirrel](https://www.fontsquirrel.com/tools/webfont-generator) 自行对它们进行 [子集化](https://www.fontsquirrel.com/tools/webfont-generator)。你甚至可以自动化您与彼得穆勒的整个工作流程 [subfont](https://github.com/Munter/subfont#readme)，一个命令行工具，静态分析，以便生成最优化的 Web 字体的子集，然后将其注入到您的网页页面。[WOFF2支持](https://caniuse.com/#search=woff2) 很棒，你可以使用 WOFF 作为不支持它的浏览器的后备。 毕竟，传统的浏览器可能会很好地使用系统字体。有许多的Web字体加载选项，你可以选择从扎克莱特曼的战略 [一个综合指南字体](https://www.zachleat.com/web/comprehensive-webfonts/)，加载策略（也可作为代码片段的 [Web字体加载配方](https://github.com/zachleat/web-font-loading-recipes)）。一般来说，使用 `preload` 资源提示预加载字体是个好主意，但在标记中包含关键 `CSS` 和 `JavaScript` 链接后的提示。否则，字体加载将花费您在第一个渲染时间。使用 [font-displayCSS描述符](https://font-display.glitch.me/)，我们可以控制字体加载行为并使内容可以立即读取（ `font-display: optional `)或几乎立即读取( `font-display: swap` ）。

#### 交付优化

1. **异步加载JavaScript**

    当用户请求页面时，浏览器获取 HTML 并构造 DOM ，然后获取 CSS 并构造 CSSOM，然后通过匹配 DOM 和 CSSOM 生成渲染树。如果需要解析任何 JavaScript，浏览器将不会开始渲染页面，直到它被解析，从而延迟渲染。作为开发人员，我们必须明确告诉浏览器不要等待并开始呈现页面。对脚本执行此操作的方法是使用 HTML 中的 `defer` 和 `async` 属性。在实践中，事实证明，我们应该更喜欢使用延迟异步。根据 [Steve Souders的说法](https://youtu.be/RwSlubTBnew?t=1034)，一旦 `async` 脚本到达，它们就会被立即执行。如果这种情况发生得非常快，例如当脚本处于缓存区时，它实际上可以阻止 HTML 解析器。在 `defer` 浏览 HTML 之前，浏览器不会执行脚本。因此，除非您在开始渲染之前需要执行 JavaScript ，否则最好使用它异步。

2. **使用 [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) 延迟加载昂贵的组件**

    一般来说，延迟加载所有昂贵的组件是个好主意，例如繁重的 `JavaScript`，`video`，`iframe`，小部件和潜在的图像。最高效的方法是使用 [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)，它提供了一种异步观察目标元素与祖先元素或顶级文档视口交叉点的变化的方法。
另外，请注意该 [lazyload属性](https://css-tricks.com/a-native-lazy-load-for-the-web-platform/)，这将允许我们 `iframe` 本地指定哪些图像和s应该是延迟加载的。[功能策略lazyload](https://www.chromestatus.com/feature/5641405942726656) 将提供一种机制，允许我们基于每个域强制选择加入或退出 [lazyload](https://css-tricks.com/a-native-lazy-load-for-the-web-platform/) 功能（类似于 [内容安全策略](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) 的工作方式）。

3. **快速推送关键 CSS**

    为了确保浏览器尽快开始渲染页面，收集开始渲染页面的第一个可见部分所需的所有 `CSS` (（称为 **关键CSS** 或 **首屏CSS** ）已成为一种 [常见做法](https://www.smashingmagazine.com/2015/08/understanding-critical-css/)）,并将其内联添加 `<head>` 到页面中，从而减少往返次数。由于在慢启动阶段交换的包的大小有限，因此关键 `CSS` 的预算约为 `14 KB`。或者，使用HTTP / 2服务器推送，但随后可能
需要创建一个缓存感知的HTTP / 2服务器推送机制。

4. **尝试重新组合 CSS 规则**

    我们已经习惯了关键的 `CSS`，但是有一些优化可以超越它。哈里·罗伯茨以非常惊人的结果进行了 [一项非凡的研究](https://csswizardry.com/2018/11/css-and-network-performance/)。例如，将主 `CSS` 文件拆分为单独的媒体查询可能是个好主意。这样，浏览器将检索具有高优先级的关键 `CSS`，以及具有低优先级的所有其他 - 完全脱离关键路径。另外，请避免 `<link rel="stylesheet" />` 在 `async` 片段之前放置。如果脚本不依赖于样式表，请考虑将阻塞脚本置于阻塞样式之上。如果他们这样做，将 `JavaScript` 拆分为两个并将其加载到 `CSS` 的任一侧。

5. **流响应**

    常常被遗忘和被忽视的，[流](https://streams.spec.whatwg.org/) 的读取或写入数据的异步块，其中只有一个子集的可能是内存可在任何给定时间提供一个接口。基本上，只要第一块数据可用，它们就允许使原始请求的页面开始使用响应，并使用针对流进行优化的解析器逐步显示内容。我们可以从多个来源创建一个流。例如，您可以让服务工作者构建一个 `shell` 来自缓存，而主体来自网络，而不是提供空的 `UI shell` 并让 `JavaScript` 填充它。正如 `Jeff Posnick` 所指出的，如果您的 `Web` 应用程序由 CMS 提供服务，该服务器通过将部分模板拼接在一起来呈现 `HTML`，则该模型直接转换为使用流式响应，模板逻辑在服务工作者而不是服务器中复制。Jake Archibald 的 [The Year of Web Streams](https://jakearchibald.com/2016/streams-ftw/) 文章重点介绍了如何构建它，性能提升非常明显。流式传输整个 `HTML` 响应的一个重要优点是，在初始导航请求期间呈现的 `HTML` 可以充分利用浏览器的流 `HTML` 解析器。在页面加载后插入到文档中的 `HTML` 块（通过 `JavaScript` 填充的内容很常见）无法利用此优化。

6. **考虑使组件连接/设备内存感知**

    数据可能很昂贵，随着负载的增加，我们需要尊重那些在访问我们的网站或应用程序时选择节省数据的用户。[保存数据客户端提示请求头](https://developers.google.com/web/updates/2016/02/save-data) 允许我们定制应用程序和负载，以限制成本和性能的用户。实际上，您可以 [将对高DPI图像的请求重写为低DPI图像](https://css-tricks.com/help-users-save-data/)，删除 web 字体、奇特的视差效果、预览缩略图和无限滚动、关闭视频自动播放、服务器推送、减少显示项的数量和降低图像质量，甚至更改交付标记的方式。此外，您还可以使用 [网络信息API](https://googlechrome.github.io/samples/network-information/) 根据网络类型交付低/高分辨率的图像和视频。[网络信息API](https://googlechrome.github.io/samples/network-information/) 和特异性 `navigator.connection.effectiveType`（ 铬62+ ）使用 `RTT`，下行，网络类型值（和一些其他）来提供的连接，以及用户可以处理数据的表示。

7. **预热连接以加快传输速度**

    使用资源提示节省时间 [dns-prefetch](https://caniuse.com/#search=dns-prefetch)（在后台执行DNS查找），[preconnect](https://www.caniuse.com/#search=preconnect) （要求浏览器在后台启动连接握手（DNS，TCP，TLS）），[prefetch](https://caniuse.com/#search=prefetch) （要求浏览器请求资源）和 [preload](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)（除了其他东西之外，它预取资源而不执行它们）。注意：如果你正在使用 `preload`，`as` 必须定义或没有加载，预加载的字体没有 `crossorigin` 属性将双倍获取。

8. **使用 Service workers 进行缓存和网络回退**

    如果您的网站是通过 HTTPS 运行的，请使用 **[实用主义者服务工作者指南](https://github.com/lyzadanger/pragmatist-service-worker)** 将静态资产缓存在服务工作者缓存中并存储脱机回退（甚至是脱机页面）并从用户的计算机中检索它们，而不是转到网络。通常，一个常见的可靠策略是将 `app shell` 与一些关键页面一起存储在服务工作者的缓存中，例如离线页面，首页以及在您的案例中可能很重要的任何其他内容。如果您正在构建一个渐进式 Web 应用程序，并且当您的服务工作者缓存从 CDN 提供的静态资产时遇到膨胀的缓存存储，请确保对于跨源资源存在正确的CORS响应头，您不会缓存不透明的响应与您的服务工作者无意中，您通过将属性添加到标记来选择跨源图像资产进入 CORS 模式。`crossorigin<img>` 使用服务工作者的一个很好的起点是 [Workbox](https://developers.google.com/web/tools/workbox/)，这是一组专门为构建渐进式 Web 应用程序而构建的服务工作者库。

9. **使用 CDN / Edge 上的 Service workers（例如，用于A / B测试）**

    此时，我们已经非常习惯在客户端上运行服务工作者，但是有了 [CDN在服务器上实现它们](https://blog.cloudflare.com/introducing-cloudflare-workers/)，我们也可以使用它们来调整边缘性能。例如，在 A / B 测试中，当 HTML 需要为不同用户改变其内容时，我们可以 [使用CDN服务器上的Service Workers](https://www.filamentgroup.com/lab/servers-workers.html) 来处理逻辑。我们还可以对 [HTML重写](https://twitter.com/patmeenan/status/1065567680298663937) 进行 [流式处理](https://twitter.com/patmeenan/status/1065567680298663937)，以加快使用Google字体的网站的速度。

10. **优化渲染性能**

    使用 [CSS包含隔离昂贵的组件](https://caniuse.com/#search=contain) -- 例如，限制浏览器样式的范围，限制画布外导航或第三方窗口小部件的布局和绘制工作。滚动页面或元素设置动画时确保没有延迟，并且您每秒都要达到 60 帧。如果这是不可能的，那么至少使每秒帧数保持一致优于 60 到 15 的混合范围。使用 CSS 的  [will-change](https://caniuse.com/#feat=will-change) 告知浏览器哪些元素和属性将改变。

11. **您是否优化了渲染体验**

    虽然组件在页面上的显示顺序以及我们如何为浏览器提供资产的策略很重要，但我们也不应低估[感知性能](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/) 的作用。在加载资产时，我们可以尝试始终领先客户一步，因此在后台发生相当多的事情时，体验会很快。为了让客户保持参与，我们可以测试 [骨架屏幕](https://twitter.com/lukew/status/665288063195594752) （实施演示）而不是加载指标，添加过渡/动画，并且在没有更多优化的情况下基本上 [欺骗用户体验](https://blog.stephaniewalter.fr/en/cheating-ux-perceived-performance-and-user-experience/)。请注意：在部署之前应该测试骨架屏幕，因为一些测试显示骨架屏幕可以通过所有指标执行最差。

#### HTTP/2

1. **为 HTTP / 2做好准备**

    随着 [Google 向更安全的网络发展](https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html)，并最终将 Chrome 中的所有 HTTP 网页视为 **不安全**，所以切换到 [HTTP / 2环境](https://http2.github.io/faq/) 是不可避免的。[HTTP / 2 得到很好的支持](https://caniuse.com/#search=http2)， 而且，在大多数情况下，你会更好。一旦在 HTTPS 上运行，您可以通过服务工作者和服务器推送（至少长期）获得显着的 [性能提升](https://www.youtube.com/watch?v=RWLzUnESylc&t=1s&list=PLNYkxOF6rcIBTs2KPy1E6tIYaWoFcG3uj&index=25)。

2. **正确部署HTTP / 2**

    您需要在打包模块和加载许多小模块之间找到一个很好的平衡点。这个平衡点就是将整个界面分解为许多小模块，然后分组，压缩
并捆绑他们。如何找到那个平衡点：如果你在 HTTP / 2 上运行，发送大约 6-10 个软件包似乎是一个不错的折衷方案（对于传统浏览器来说并不算太糟糕）。尝试和衡量为您的网站找到合适的平衡点。

3. **您的服务器和 CDN 是否支持 HTTP / 2**

    不同的服务器和 CDN 可能会以不同的方式支持 HTTP / 2。快速使用  [TLS](https://istlsfastyet.com/) 检查您的选项，或快速查找服务器的性能以及可以支持的功能。
请参阅 Pat Meenan 对 [HTTP / 2优先级](https://blog.cloudflare.com/http-2-prioritization-with-nginx/) 和 [测试服务器支持HTTP / 2优先级](https://github.com/pmeenan/http2priorities) 的令人难以置信的研究。根据 Pat 的说法，建议启用 BBR 拥塞控制并将其设置 `tcp_notsent_lowat` 为 16KB 以进行 HTTP / 2 优先级排序，以便在 Linux 4.9 内核及更高版本上可靠地运行（感谢Yoav！）。Andy Davies对跨浏览器，[CDN和云托管服务的 HTTP / 2优先级](https://github.com/andydavies/http2-prioritization-issues#cdns--cloud-hosting-services) 进行了类似的研究。

4. **是否启用了 OCSP 装订**

    通过 [在服务器上启用OCSP装订](https://www.digicert.com/enabling-ocsp-stapling.htm)，可以加快 TLS 握手速度。创建在线证书状态协议（OCSP）作为证书撤销列表（CRL）协议的替代方案。两种协议都用于检查 SSL 证书是否已被撤销。但是，OCSP 协议不要求浏览器花时间下载然后在列表中搜索证书信息，从而减少握手所需的时间。

5. **你有没有采用 IPv6**

    由于我们的 [IPv4空间不足](https://en.wikipedia.org/wiki/IPv4_address_exhaustion)，主要移动网络正在迅速采用 IPv6（美国已经达到了 50％ 的 IPv6 采用率阈值），因此最好 [将DNS更新为IPv6](https://blog.paessler.com/ask-the-expert-current-status-on-ipv6) 以保证未来的防范。只需确保通过网络提供双栈支持 - 它允许 IPv6 和 IPv4 同时并行运行。毕竟，IPv6 不是向后兼容的。此外，有 [研究表明](https://www.cloudflare.com/ipv6/)，由于邻居发现（NDP）和路由优化，IPv6 使这些网站的速度提高了 10％ 到 15％。

6. **是否正在使用 HPACK 压缩**

    如果您使用的是 HTTP / 2，请仔细检查您的服务器是否为HTTP响应标头 [实施HPACK压缩](https://blog.cloudflare.com/hpack-the-silent-killer-feature-of-http-2/)，以减少不必要的开销。由于 HTTP / 2 服务器相对较新，它们可能不完全支持规范， HPACK 就是一个例子。[H2spec](https://github.com/summerwind/h2spec) 是一个很好的（如果非常技术详细）工具来检查。HPACK 的压缩算法令人印象深刻，而且很有效。

7. **确保服务器上的安全性是防弹的**

    HTTP / 2 的所有浏览器实现都通过 TLS 运行，因此您可能希望避免安全警告或页面上的某些元素无法正常工作。仔细检查您的 [安全标头是否设置正确](https://securityheaders.com/)，[消除已知漏洞](https://www.smashingmagazine.com/2016/01/eliminating-known-security-vulnerabilities-with-snyk/) 并 [检查您的证书](https://www.ssllabs.com/ssltest/)。此外，请确保通过HTTPS加载所有外部插件和跟踪脚本，无法进行跨站点脚本编写，并且正确设置了 [HTTP严格传输安全标头](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) 和 [内容安全策略标头](https://content-security-policy.com/)。

#### 测试和监测

1. **监控混合内容警告**

    如果您最近从HTTP迁移到HTTPS，请确保同时监控活动和
使用Report-URI.io等工具进行被动混合内容警告。你也可以使用混合
内容扫描启用HTTPS的网站以查找混合内容。

2. **您是否优化了审计和调试工作流程**

    这可能听起来不是什么大问题，但在指尖设置合适的设置可能会为您节省大量的测试时间。考虑使用 Tim Kadlec 的 [WebPageTest](https://github.com/tkadlec/webpagetest-alfred-workflow) 中的 [Alfred Workflow](https://github.com/tkadlec/webpagetest-alfred-workflow) 将测试提交给 [WebPageTest](https://github.com/tkadlec/webpagetest-alfred-workflow) 的公共实例。您还可以从 [Google电子表格中驱动WebPageTest](https://calendar.perfplanet.com/2014/driving-webpagetest-from-a-google-docs-spreadsheet/) ，并将可访问性，性能和 SEO 分数纳入您使用 `Lighthouse CI` 的 `Travis` 设置或 [直接进入Webpack](https://twitter.com/addyosmani/statuses/1017655423099289600)。

3. **您是否在代理浏览器和旧版浏览器中测试过**

    在 Chrome 和 Firefox 中进行测试是不够的。了解您的网站在代理浏览器和旧版浏览器中的工作方式。例如，UC浏览器 和 Opera Mini 在亚洲占有很大的市场份额（ **亚洲高达35％** ）。测量您感兴趣的国家/地区的 [平均互联网速度](https://www.webworldwide.io/)，以避免出现重大意外情况。使用网络限制进行测试，并模拟高DPI设备。[BrowserStack](https://www.browserstack.com/) 非常棒，但也可以在真实设备上进行测试。

4. **是否建立了连续监控**

    拥有 [WebPagetest](https://www.webpagetest.org/) 的私有实例总是有利于快速和无限制的测试。但是，具有自动警报功能的连续监控工具（如 [Sitespeed](https://www.sitespeed.io/)， [Calibre](https://calibreapp.com/) 和 [SpeedCurve](https://speedcurve.com/) ）将为您提供更详细的 [性能图表](https://speedcurve.com/)。设置您自己的用户计时标记，以衡量和监控特定于业务的指标。此外，请考虑添加 [自动性能回归警报](https://calendar.perfplanet.com/2017/automating-web-performance-regression-alerts/) 以监控一段时间内的变化。研究使用 RUM 解决方案来监控性能随时间的变化。对于自动化的单元测试相似的负载测试工具，您可以将 [k6](https://github.com/loadimpact/k6) 与其脚本 API 一起使用。另外，请查看 [SpeedTracker](https://speedtracker.org/)，[Lighthouse](https://github.com/GoogleChrome/lighthouse) 和 [Calibre](https://calibreapp.com/)。

#### 快速核查

此列表非常全面，完成所有优化可能需要一段时间。那么，如果你只有1小时的时间来获得重大改进，你会做什么？让我们把它煮成12个低悬的水果。显然，在开始之前和完成之后，测量结果，包括在3G和电缆连接上开始渲染时间和速度指数。

1. 衡量现实世界的经验并设定适当的目标。一个很好的目标是第一个有意义的油漆<1秒，速度指数值<1250，慢速3G上交互时间<5秒，重复访问时间，TTI <2s。优化开始渲染时间和交互时间。
2. 为主模板准备关键CSS，并将其包含在 `<head>` 页面中。（您的预算为14 KB）。对于CSS / JS，在最大的关键文件大小预算内运行。170KB gzipped（0.7MB解压缩）。。
3. 尽可能多地修剪，优化，推迟和延迟加载脚本，检查轻量级备选方案并限制第三方脚本的影响。
4. 仅将遗留代码提供给旧版浏览器 `<script type="module">`。
5. 尝试重新组合CSS规则并测试体内CSS。
6. 添加资源提示以加快交付速度，加快dns查找，预连接，预取和预加载。
7. 子集Web字体并异步加载它们，并在CSS中快速使用字体显示渲染。
8. 优化图像，并考虑将WebP用于关键页面（例如登录页面）。
9. 检查是否正确设置了HTTP缓存头和安全头。
10. 在服务器上启用Brotli或Zopfli压缩。 （如果那不可能，请不要忘记启用
Gzip压缩。）
11. 如果HTTP / 2可用，请启用HPACK压缩，并开始监视混合内容
警告。启用OCSP装订。
12. 如果可能，在服务工作缓存中缓存诸如字体，样式，JavaScript和图像之类的资产。

非常感谢Guy Podjarny，Yoav Weiss，Addy Osmani，Artem Denysov，Denys Mishunov，Ilya Pukhalski，
Jeremy Wagner，Colin Bendell，Mark Zeman，Patrick Meenan，Leonardo Losoviz，Andy Davies，Rachel Andrew，
Anselm Hannemann，Patrick Hamann，Andy Davies，Tim Kadlec，Rey Bango，Matthias Ott，Peter Bowyer，Phil
Walton，Mariana Peralta，Philipp Tellis，Ryan Townsend，Ingrid Bergman，Mohamed Hussain S H，Jacob
Groß，Tim Swalling，Bob Visser，Kev Adamson，Adir Amsalem，Aleksey Kulikov和Rodney Rehm。
回顾这篇文章，以及我们精彩的社区，它们分享了技术和经验教训
从它在性能优化方面的工作，供大家使用。 你真是赢了！

