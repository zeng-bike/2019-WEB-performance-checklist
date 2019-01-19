正文之前：首先介绍一下我自己，一个跨行业的，完全非科班生的文科生。通过半自学，半跟班的方式在一路摸索的过程中终于算是入了前端的这个门。这篇文章是自己参加掘金主编Linmi发起的一个2019年度开发者写作计划活动中，跟着活动计划者一起翻译的。
```
    原文链接地址：https://www.smashingmagazine.com/2019/01/front-end-performance-checklist-2019-pdf-pages/
    本文译自维塔利弗里德曼的前端性能优化清单的文章--2019篇幅。
    这是一篇有关年度前端性能检查的文章，包含了创建快速体验所需的所有知识，自2016年以来每年更新一次。
```

Web性能在前端领域是一个棘手的问题，所以，知道我们在性能方面处于什么位置，以及我们的性能瓶颈究竟是什么就显得更为重要了。它是昂贵的 JavaScript 呢、 还是缓慢的 web 字体传递、 或是较大的图片在使得页面加载速度变缓？web性能优化包括：无用代码移除 （Tree-shaking）、作用域提升（Scope hoisting）、代码分割（Code-spliting），交叉观察器（Intersection observer）、服务器推送（server push）、客户端提示（clients hints）、HTTP/2、service workers 等等这些手段。然而，最重要的是，我们该 **从哪里开始提高前端性能** 以及 **如何建立长久的前端性能优化机制**？

之前，我们习惯性在完成项目之后，再去考虑前端方面的性能优化。这样就会导致留给我们优化的时间极度有限，让我们不得不缩小优化考虑的范围。通常我们优化的内容也局限于资源优化（一些静态文件的缩小）和服务器配置文件上的一些细微调整。现在回过来看，前端发展越来越快，涉及面越来越广，性能优化光做到这些还是远远不够的。

性能不仅仅是一个技术问题：它很重要，所以当将其放入工作流中时，我们必须根据性能的影响来做设计决策。性能必须被测量、监测和不断的完善。网络日益增长的复杂性也使得前端性能指标的跟踪变得越来越难，因为性能指标会根据设备、浏览器、协议、网络类型和延迟而发生改变（CDN、ISP、缓存、代理、防火墙、负载均衡器和服务器都在性能方面发挥作用）。

因此，我们创建了一个在提高性能时必须记住的所有事情的概述：即从网站的最开始准备阶段到网站的最终发布需要注意的性能问题列表。以下是2019年的前端性能优化清单（希望没有偏见和客观）—— 更新了您可能需要考虑的问题，以确保您的网站响应时间更快，用户交互更加流畅，不会占用用户的带宽。


## 目录
* 计划和度量
* 制定现实的目标
* 定义环境
* 资源优化
* 构建优化
* 交互优化
* HTTP / 2
* 测试和监测
* 速效方案

（您也可以仅下载 [前端性能优化清单的 PDF 版本](https://www.dropbox.com/s/21vof23jlwf0swc/performance-checklist-1.2.pdf?dl=0)（166 kb）或者 [下载 Apple Pages 版本](https://www.dropbox.com/s/xyf5qjnp1ii5okm/performance-checklist-1.2.pages?dl=0)（275 kb）或者是 [.docx 文件](https://www.dropbox.com/s/76b3yzexqdwsg65/performance-checklist-1.2.docx?dl=0) (151 kb)。祝愿大家，在前端性能优化这条路上走的越来越顺畅！！！）

### 准备：计划和度量

微优化对于保持性能的正常运行非常重要，所以在我们必须把明确的目标时刻印记在脑海中。明确的目标应该是可以度量，因为他可以影响整个过程中所做的任何决策。这里有几种不同的模式，我们需要从自身的角度出发，尽早确认自己项目中性能优化的优先级别。

1. **建立性能优化意识**

    在很多技术团队中，前端开发人员确切地知道什么是常见的底层问题，以及应该使用什么加载模式来修复这些问题。然而，只要没有对性能优化的意见达成一致，每个部门就会按照自己的理解来定位产品，这样一个公司就会变成一盘散沙。这时候，需要让相关人员都参与进来， 然后建立一个调查问卷，调查大家所关心的速度效益指标和关键性能指标( kpi )。
    
    如果开发/设计部与业务部之间的意见还没有达成一致，那么性能优化将无法开展。研究用户在体验产品之后的反馈，看看如何提高性能以助于解决这些常见问题。
    
    在移动设备和桌面设备上运行性能实验并测量结果，得到的真实的数据将帮助你建立一个为公司量身定制的案例研究。此外，使用 [WPO Stats](https://wpostats.com/) 上发布的案例研究和实验数据，可以帮助提高你对性能和业务之间的潜在关系的认识，以及性能对用户体验和业务度量的影响。仅仅说明性能很重要是不够的，您还需要建立一些可度量的、可跟踪的目标来观测性能。
    
    Allison McKnight 在她关于 [构建长期性能优化](https://vimeo.com/album/4970467/video/254947097) 的演讲中分享了她如何帮助 Etsy 建立性能优化的全面案例研究。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/15/1685097e5533c579?w=2634&h=730&f=png&s=163686)
    [性能优化创建者](http://bradfrost.com/blog/post/performance-budget-builder/) 布拉德·弗罗斯特和乔纳森·菲尔丁 [性能优化计算器](http://www.performancebudget.io/) 可以帮助您设置性能需要优化到的大小。

2. **目标：要比你最快的竞争对手快至少 20%**

    根据心理学研究，如果你想让用户觉得你的网站比竞争对手的网站快，你需要至少快20%。研究你的主要竞争者，收集他们在移动端和桌面上的性能，并且设置一个你能超过他们的临界值。要获取准确的结果和目标，首先要研究你的分析结果，看看你的用户都在做什么。然后，您可以模拟第90个百分位的测试经验。
    
    为了更好地了解竞争对手的表现，您可以使用 [Chrome UX报告](https://web.dev/fast/chrome-ux-report)（ CrUX，现成的 RUM 数据集，Ilya Grigorik 的 [视频介绍](https://vimeo.com/254834890)），[Speed Scorecard](https://www.thinkwithgoogle.com/feature/mobile/)（也提供收入影响估算器）， [真实用户体验测试比较](https://ruxt.dexecure.com/compare) 或 [SiteSpeed CI](https://www.sitespeed.io/)（基于综合测试）。
    
    **注意**：如果使用 [Page Speed Insights](https://developers.google.com/speed/pagespeed/insights/)（不推荐使用），则可以获取特定页面的 CrUX 性能数据，而不仅仅是聚合。此数据对于设置 **目标网页** 或 **产品详情** 等资产的效果目标非常有用。如果您使用 CI 来测试预算 以及 CrUX 设置目标，则需要确保您的测试环境与 CrUX 匹配（感谢Patrick Meenan！）。
    
    收集数据之后，建立一个[电子表格](http://v3.danielmall.com/articles/how-to-make-a-performance-budget/)，将数据结果减去20%就是你的目标（即 [性能预算](http://bradfrost.com/blog/post/performance-budget-builder/)）。现在，你在测试之前就有了一些可度量的数据。在这个数据（性能预算）的前提下，尝试使用最少的脚本来实现最快的交互，这样子我们就算是达成了自己的目标。
    
    启动所需要的资源：
    - Addy Osmani 写了一篇关于[如何开始性能预算](https://medium.com/@addyosmani/start-performance-budgeting-dabde04cf6a3)、如何量化新特性的影响以及在超出预算时从何处开始的非常详细的文章。
    - Lara Hogan [关于如何使用性能预算进行设计](http://designingforperformance.com/weighing-aesthetics-and-performance/#approach-new-designs-with-a-performance-budget) 的指南可以为设计师提供有用的指导。
    - Jonathan Fielding 的 [性能预算计算器](http://www.performancebudget.io/)、Brad Frost 的 [性能预算构建器](https://codepen.io/bradfrost/full/EPQVBp/) 和[浏览器卡路里](https://browserdiet.com/calories/) 可以帮助创建预算(感谢 [Karolina Szczur](https://medium.com/@fox/talk-the-state-of-the-web-3e12f8e413b3) 的领导)。
    - 此外，通过使用报告构建大小的图表设置仪表板，可以使性能预算和当前性能可见。有许多工具可以帮助您实现这一目标：[SiteSpeed.io](https://www.peterhedenskog.com/blog/2015/04/open-source-performance-dashboard/) 仪表板（开源），[SpeedCurve](https://speedcurve.com/) 和 [Calibre](https://calibreapp.com/) 只是其中的一部分，您可以在 [perf.rocks](http://perf.rocks/tools/) 上找到更多工具。
    
    准备好预算后，使用 [Webpack Performance Hints](https://web.dev/fast/incorporate-performance-budgets-into-your-build-tools) 和 [Bundlesize](https://web.dev/fast/incorporate-performance-budgets-into-your-build-tools)，[Lightouse CI](https://web.dev/fast/using-lighthouse-ci-to-set-a-performance-budget)，[PWMetrics](https://github.com/paulirish/pwmetrics) 或 [Sitespeed CI](https://www.sitespeed.io/) 将它们合并到构建过程中，以强制执行拉取请求的预算并在PR注释中提供分数历史记录。如果你需要自定义的东西，你可以使用 [webpagetest-charts-api](https://github.com/trulia/webpagetest-charts-api)，一个端点 API 来自 WebPagetest 结果构建图表。
    
    例如，就像 [Pinterest](https://medium.com/@Pinterest_Engineering/a-one-year-pwa-retrospective-f4a2f4129e05) 一样，您可以创建一个自定义的 `eslint` 规则，该规则禁止从已知属于依赖性的文件和目录中导入并使该捆绑包膨胀。设置可在整个团队中共享的 **安全** 软件包列表。
    
    除了性能预算之外，还要考虑对您的业务最有利的关键客户任务。设置并讨论 **关键操作的** 可接受 **时间阈值**，并建立整个组织已达成一致的 **UX就绪** 用户时间标记。在许多情况下，用户旅程将涉及许多不同部门的工作，因此在可接受的时间安排方面的协调将有助于支持或阻止绩效讨论。确保可以看到和理解添加的资源和功能的额外成本。
    
    此外，正如 Patrick Meenan 所建议的那样，最好在设计的过程中设置一个加载队列并且要知道这些顺序会存在哪些利弊。您需要优先处理更重要的优先级，并定义它们应该出现的顺序，那么您就可以确定哪一部分可以延迟。通常理想情况下，该队列也反映 `CSS` 和 `JavaScript` 导入的顺序，因此在构建过程中处理它们会更容易。此外，在加载页面时（例如，当尚未加载 Web 字体时），考虑视觉体验应该在 **中间** 状态中。
    
    规划、计划、规划,重要的事情说三遍。如果早期进行优化那么会很容易实现目标，但是没有计划或者没有制定切合实际的、为公司量身定制的业绩目标，那么就很难保持性能。

3. **选择正确的指标**

    [不是所有的度量都很重要](https://speedcurve.com/blog/rendering-metrics/)。研究哪些度量对于你的应用程序最重要：通常，这与你能够以多快的速度开始渲染最重要的像素（以及它们的效果）以及如何为这些渲染像素提供输入最快的响应速度有关。 这可以帮助你为后续的工作提供最佳的优化结果。
    
    不管怎样，不要专注于整个页面的加载时间（例如 `onLoad` 和 `DOMContentLoaded` 时间），而是要优先按照用户可以感知到的页面加载。 也就是说要关注一组稍微不同的度量。
    
    根据 Tim Kadlec 的研究和 Marcos Iglesias 在他的 [演讲](https://docs.google.com/presentation/d/e/2PACX-1vTk8geAszRTDisSIplT02CacJybNtrr6kIYUCjW3-Y_7U9kYSjn_6TbabEQDnk9Ao8DX9IttL-RD_p7/pub?start=false&loop=false&delayms=10000&slide=id.g3ccc19d32d_0_98) 中所做的笔记，传统的度量指标可以分为几种。通常情况下，我们在全面了解性能的时候可能需要用到所有的这些方法，但是，也有可能在自己实际的项目当中，其中的某一种方法比其他方法更为重要。
    
    这里挑出一些相对更为重要的方法：
    - **基数度量标准**（Quantity-based metrics）主要是用来衡量请求数量，权重和性能的得分。适用于一些提高警报或者监控随着时间的变化而改变的项目，但是对于用户体验不是很友好。 
    - **里程碑度量标准**（Milestone metrics）指的是项目在加载过程中，项目在某个生命周期中一个使用状态，例如：到某个生命节点所需要的时间，或者是完成某个交互所需要的时间。虽然这个度量标准不会记录两个不同生命周期之间发生的事情，但是却适合用来监控和描述用户的体验。
    - **渲染度量标准**（Rendering metrics）是用来预估页面内容呈现的速度。适合用于测量和调整渲染性能，但不适合用来测量重要内容在什么时间节点出现并可与之进行交互。
    - **自定义度量标准**（Custom metrics） 是用来衡量项目的特定自定义事件。例如 Twitter 的 [Time To First Tweet](https://blog.alexmaccaw.com/time-to-first-tweet) 和 Pinterest 的 [PinnerWaitTime](https://medium.com/@Pinterest_Engineering/driving-user-growth-with-performance-improvements-cfc50dafadd7)。适合用于精确的描述用户的体验，不太适合根据这个标准来和对手进行比较。
    
    下面罗列一些最具体和相关的的度量标准：
    * **首次有效渲染时间** -- First Meaningful Paint （FMP）指的是主要内容出现在页面上的时间，让您深入了解服务器输出任何数据的速度。Long FMP 大部分表示 JavaScript 阻塞了主线程，当然也可能是后端或者服务器的问题导致的。
    * **交互时间** （TTI）是指页面布局已经稳定，关键的页面字体已经可见，主进程足以去处理用户的输入 —— 用户可以在 UI 上进行点击和交互的基本时间标记。用来了解用户在没有延迟的情况下打开网站需要多长的时间。
    * **输入响应** （FID）即接口响应用户在实现交互操作所需的时间。
    * **速度指数** -- Speed Index 测量页面内容在视觉上的填充速度，得分越低越好。速度指数得分是根据视觉进度的速度计算的，它只是一个计算值，对于视觉窗口大小很敏感，所以您需要定义一个与大众相匹配的测试标准（感谢，Boris！）。
    * **CPU时间花费** 指的是CPU时间一个度量，指示主线程处理有效负载的繁忙程度。它显示了主线程被阻止的频率和持续时间，用于绘制，渲染，编写脚本和加载。根据janky的经验，高CPU时间即表示用户遇到他们的行动和反应之间存在明显的滞后。使用 WebPageTest，您可以 [在 Chrome 选项卡上选择 Capture Dev Tools Timeline](https://deanhume.com/ten-things-you-didnt-know-about-webpagetest-org/)，以显示主线程使用 WebPageTest 在任何设备上运行时的详细分数。
    * **[广告权重影响](https://calendar.perfplanet.com/2017/measuring-adweight/)** 如果您的网站主要收入来源于广告，那么与广告业务模块的代码就要特别关注。Paddy Ganti 的 [脚本](https://calendar.perfplanet.com/2017/measuring-adweight/) 构造了两个URL（一个是正常的URL，一个阻止广告的URL），提示通过 WebPageTest 生成视频比较并报告增量。
    * **偏差度量标准** 一个仪器的测量结果的数据可以让我们知道这个仪器的可靠性，同理，我们可以通过测试的出来的数据结果分析，然后做出一个平衡。数据结果中，差异很大的标准需要重新设置，并且他还有助于我们了解某些页面是否会因为某些其他原因（，例如第三方脚本）而导致更难以可靠地测量。另外，在推出新的浏览器版本时，对比新版本与旧版本在性能上的差异也是度量偏差的一个好方法。
    * **[自定义度量标准](https://speedcurve.com/blog/user-timing-and-custom-metrics/)** 即由您的业务需求和客户体验来定义。它要求您解析重要像素，关键脚本，必要的  CSS 和其他的相关资源，并预测页面展现在用户视觉下的速度。对于这个标准，您可以监视 [Hero渲染时间](https://speedcurve.com/blog/web-performance-monitoring-hero-times/)，或使用 [Performance API](https://css-tricks.com/breaking-performance-api/)，为业务中很重要的事件标记一个时间戳。此外，您可以通过在测试结束时执行任意 JavaScript，[然后通过结果对照 WebPagetest 确定自定义指标](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/custom-metrics)。
    
    Steve Souders [详细的解释了每个度量](https://speedcurve.com/blog/rendering-metrics/)。在许多情况下，我们测量出的数据是在特定环境下的使用程序得出的数据，但是输入响应代表的是用户的实际体验，实际当中，用户的体验要明显滞后。所以，保持持续测量和收集用户行为对于度量的制定相对来说更准确。
    
    根据应用程序的上下文，首选度量可能会有所不同：例如，对于 Netflix TV UI：输入响应，[内存使用](https://medium.com/netflix-techblog/crafting-a-high-performance-tv-user-interface-using-react-3350e5a6ad3b) 和 TTI 更为关键，对于维基百科，[第一个/最后一个视觉更改和CPU时间花费度量](https://phabricator.wikimedia.org/phame/live/7/post/117/performance_testing_in_a_controlled_lab_environment_-_the_metrics/)更为重要。
    
    注意：FID 和 TTI 都不考虑滚动行为; 滚动可以独立发生，因为它是非主线程，因此对于许多内容消费网站而言，这些指标可能相对于没有那么重要。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/18/1685fc68a4182f74?w=1288&h=620&f=png&s=51074)
    以用户为中心的性能指标可以更好地洞察实际的用户体验。[输入响应](https://developers.google.com/web/updates/2018/05/first-input-delay)（FID）是一种尝试实现这一目标的新度量(感谢Patrick!)。

4. **从具有代表性的用户使用的设备收集数据**

    为了收集准确的数据，我们需要尽可能全的选择要测试的设备。最好是 Moto G4，或者一款中档的三星设备又或者是一个 Nexus 5X 这样的普通的设备。如果你手边没有设备，可以使用节流 CPU（5× 减速）来限制网速（例如，150 ms 的往返时延，1.5 Mbps 以下和0.7 Mbps 以上）实现在桌面设备上模拟移动设备的体验。最终，切换到常规的 3G，4G 和 Wi-Fi。为了使性能体验的影响更明显，你甚至可以使用 2G 或 一个节流的 3G 网络，以便进行更快的测试。
    
    幸运的是，有很多优秀的选项可以帮助你自动收集数据，并根据这些度量衡量你的网站在一段时间内的性能。 请记住，良好的性能度量是需要被动和主动监控工具的组合：
    - **被动监测工具，可以根据请求来模拟用户交互（综合测试，如Lighthouse，WebPageTest）**
    - **主动监测工具，**是那些不断记录和评价用户交互行为的（**真正的用户监控**，如 **SpeedCurve**，**New Relic** —— 这两种工具也提供综合测试）
    
    前者在开发过程中特别有用，因为它可以在使用产品时持续跟踪。 后者在长期维护非常有用，因为它可以帮助你了解在实际访问站点时发生的性能瓶颈。通过使用导航定时、资源定时、绘图定时、长时间任务等内置的 RUM API，被动和主动性能监视工具一起提供应用程序性能的完整画面。 例如，你可以使用 [PWMetrics](https://github.com/paulirish/pwmetrics)，[Calibre](https://calibreapp.com/)，[SpeedCurve](https://speedcurve.com/)，[mPulse](https://www.soasta.com/performance-monitoring/)，[Boomerang](https://github.com/yahoo/boomerang) 和 [Sitespeed.io](https://www.sitespeed.io/)，这些都是性能监测工具的绝佳选择。
    
    注意：选择浏览器外部的网络级别的限制器总是比较安全的，例如 DevTools 由于实现的方式而存在与 HTTP/2 推送交互的问题（感谢Yoav！）。

5. **设置干净的用户配置文件以进行测试**

    在监视工具中测试时，需要关闭防病毒和后台CPU任务，删除后台带宽传输以及使用干净的用户配置文件。我们需要注意的是，防止使用浏览器（Firefox，Chrome）扩展而导致结果出现偏差
    
    有时候，研究客户经常使用的扩展程序以及使用专用的客户配置文件进行测试也是一个好主意。在实际应用当中，如果您的用户经常使用它们，您可能需要优先考虑到它，因为某些扩展可能会对您的应用程序产生很大的性能影响。我们对于**干净**的个人资料结果过于乐观，因为在实际的用户应用场景中可能会被粉碎。

6. **与同事分享性能清单**

    为了避免误解，要确保你团队里的每个同事都对清单很熟悉。每个决策都对性能有影响。项目将极大地受益于前端开发人员正确地将性能价值传达给整个团队。从而使每个人都对它负责，而不仅仅是前端开发人员。根据绩效预算和清单中定义的优先顺序来设计决策。

### 制定现实的目标

7. **响应时间控制在 100ms，帧速控制在 60帧/秒**

    为了让交互感觉起来很顺畅，接口有 100ms 来响应用户的输入。任何比这更长的时间，都会让用户感觉到应用程序很慢。 [RAIL，一个以用户为中心的性能模型](https://www.smashingmagazine.com/2015/10/rail-user-centric-model-performance/) 会为你设立一个正确的目标：要达到 < 100ms 响应时间的目标，页面必须要在小于 50ms 前最迟将控制权返回给主线程。[预计输入延迟](https://developers.google.com/web/tools/lighthouse/audits/estimated-input-latency) 时间告诉我们，如果我们能达到这个门槛，那么在理想情况下，它应该低于 50ms。对于像动画这样性能消耗比较大的地方，最好的做法是，在能够优化的地方，尽量优化到极致；在不能优化的地方，让性能开销降至最低。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/18/168602f5898c9191?w=2000&h=725&f=png&s=37038)
    [RAIL](https://developers.google.com/web/fundamentals/performance/rail)，一种以用户为中心的性能模型。
    
    同时，每一帧动画应该要在 16 毫秒内完成，从而达到 60 帧每秒（1秒 ÷ 60 = 16.6 毫秒） —— 最好可以在 10 毫秒完成。因为浏览器需要时间将新框架绘制到屏幕上，你的代码应该在触发 16.6 毫秒以内完成。[在页面设计上保持乐观](https://www.smashingmagazine.com/2016/11/true-lies-of-optimistic-user-interfaces/) 和 [明智地利用空闲时间](https://philipwalton.com/articles/idle-until-urgent/)。显然，这些目标适用于运行时的性能，而不是加载性能。

8. **速度指标（SpeedIndex） < 1250，3G上的交互时间（Interaction time）小于5s，关键文件大小预算 < 170 Kb（gzip）**

    虽然这可能很难实现，一个好的最终目标是首次有效渲染低于 1s 并且 [SpeedIndex](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index) 的值低于 1250。因为我们是以 200 美金为基准的 Android 手机（如 Moto G4）和一个缓慢的 3G 网络上，模拟 400ms 的往返延时和 400kb 的传输速度，所以我们的目标是 [可交互时间低于5s](https://www.youtube.com/watch?v=_srJ7eHS3IM&feature=youtu.be&t=6m21s)，并且再次访问的时间低于 2s。
    
    请注意，当谈到可交互时间时，最好来 [区分一下首次交互(First CPU Idle)和 连续交互(Time To Interactive)](https://calendar.perfplanet.com/2017/time-to-interactive-measuring-more-of-the-user-experience/) 以避免对它们之间的误解。前者是在主要内容已经渲染出来后最早出现的点（窗口至少需要 5s，页面才开始响应）。后者是期望页面可以一直进行输入响应的点。
    
    HTML 的前 14~15kb 加载是是最关键的有效载荷块—— 也是第一次往返（这是在400 ms 往返延时下 1 秒内所得到的）预算中唯一可以交付的部分。一般来说，为了实现上述目标，我们必须在关键的文件大小内进行操作。最高预算压缩之后 170 Kb（0.8-1MB解压缩），它已经占用多达 1s （取决于资源类型）来解析和编译。稍微高于这个值是可以的，但是要尽可能地降低这些值。
    
    尽管如此，还是可以提高绑定的规模预算。例如，你可以在浏览器主线程的活动中设置性能预算，例如，在开始渲染前的绘制时间或者 [跟踪前端 CPU](https://calendar.perfplanet.com/2017/tracking-cpu-with-long-tasks-api/)。像 [Calibre](https://calibreapp.com/)，[SpeedCurve](https://speedcurve.com/) 和 [Bundlesize](https://github.com/siddharthkp/bundlesize) 这些工具可以帮助你保持你的预算控制，并集成到你的构建过程。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/18/16860415acee154f?w=2000&h=1118&f=jpeg&s=63488)
    [From Fast默认](https://speakerdeck.com/addyosmani/fast-by-default-modern-loading-best-practices)： Addy Osmani的[现代加载最佳实践](https://speakerdeck.com/addyosmani/fast-by-default-modern-loading-best-practices)。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/18/16860b9c83062ab7?w=2000&h=1000&f=jpeg&s=95708)
    [性能预算应根据普通移动设备的网络条件进行调整](https://twitter.com/katiehempenius/status/1075478356311924737)。（图片来源：Katie Hempenius）

### 定义环境

9. **根据实际情况选择并搭建构建工具**

    [不要把太多的关注点放在那些看起来很酷的构建工具上](https://2018.stateofjs.com/)。根据您的项目来构建环境，无论是Grunt、Gulp、Webpack、Parcel，还是工具组合。只要这个构建工具能够让您快速的得到结果，并且保证您的构建过程没有问题，那么您就可以选择该构建工具。
    
    在所有的构建工具中，Webpack似乎是最成熟的一个，它有数百个插件可以用来优化构建的大小。如果你作为一位初用者，刚开始使用Webpack可能会很困难。所以如果你想开始使用 webpack，下面有一些很好的资源可以给您指引:
    
    - [Webpack文档](https://webpack.js.org/concepts/) 是一个很好的入手点，同样 [Webpack](https://medium.com/@rajaraodv/webpack-the-confusing-parts-58712f8fcad9)相关的文章也可以作为很好的入门指引：Raja Rao 的 [Confusing Bits]() 和 [Andrew Welch](https://medium.com/@rajaraodv/webpack-the-confusing-parts-58712f8fcad9) 的 [Annotated Webpack Config](https://nystudio107.com/blog/an-annotated-webpack-4-config-for-frontend-web-development)。
    - Sean Learkin 上有一个关于 [Webpack](https://webpack.academy/p/the-core-concepts) 的免费课程: [Core Concepts](https://webpack.academy/p/the-core-concepts)，Jeffrey Way 也发布了一个关于 [Webpack](https://laracasts.com/series/webpack-for-everyone) 的免费精彩视频供大家学习。它们都是深入的介绍了 [Webpack](https://laracasts.com/series/webpack-for-everyone)。
    - [Webpack Fundamentals](https://frontendmasters.com/courses/webpack-fundamentals/) 是一个非常全面的4小时课程，由 FrontendMasters 发布在 Sean Learkin。
    - 如果您对 Webpack 已经有初步的了解，Rowan Oulton 发布了一个使用 Webpack 获得 [更好构建性能](https://slack.engineering/keep-webpack-fast-a-field-guide-for-better-build-performance-f56a5995e8f1) 的 [应用场景指南](https://slack.engineering/keep-webpack-fast-a-field-guide-for-better-build-performance-f56a5995e8f1)，Benedikt Rotsch 对如何[将Webpack绑定在一个节点上](https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/) 进行了深入的研究。
    - [Webpack示例](https://github.com/webpack/webpack/tree/master/examples) 包含了数百个即用型 Webpack 配置，主要按主题和用途分类。另外，还有一个 [Webpack Config 配置器](https://webpack.jakoblind.no/)，可以生成一个基本配置文件。
    - [awesome-webpack](https://github.com/webpack-contrib/awesome-webpack) 是一个非常有用的关于 Webpack 资源、库和工具的列表，里面包括一些介绍Angular、React和未使用框架项目的文章、视频、课程、书籍和示例。

10. **默认情况下使用渐进增强**

    安全的选择是将渐进增强作为前端架构和项目部署的指导原则。首先设计和构建核心体验，然后通过功能强大的浏览器的高级功能增强体验，创造 [弹性](https://resilientwebdesign.com/) 体验。如果你的网站在一个网络不佳、糟糕设备、性能差的低版本浏览器上运行速度还是挺快，那么这个网站在一个网络环境好、设备和浏览器性能都比较好的环境下会运行起来会更加快。

11. **选择强大的性能基准**

    有这么多的未知影响加载 —— 网络、热节流、缓存回收、第三方脚本、解析器阻塞模式、磁盘的读写、 IPC jank、插件安装、CPU、硬件和内存限制、L2/L3缓存、RTTS、图像、Web字体加载行为的差异，[其中 Javascript 脚本的代价是最大的](https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4)，Web 字体阻塞默认的渲染和图片的加载使得内存消耗太大。随着性能瓶颈 [从服务器端转移到客户端](https://calendar.perfplanet.com/2017/tracking-cpu-with-long-tasks-api/)，作为开发人员，我们必须更仔细地考虑所有这些未知因素。
    
    在 170kb 的预算中，已经包括了关键路径的 HTML / CSS / JavaScript、路由器、状态管理、实用程序、框架和应用程序逻辑，我们必须彻底 [检查网络传输成本，解析/编译时间和运行时间](https://www.twitter.com/kristoferbaxter/status/908144931125858304)来选择我们的框架。
    
    Seb Markbage [指出](https://twitter.com/sebmarkbage/status/829733454119989248)，衡量框架启动成本的最好的方法就是先渲染视图，然后删除，然后再渲染，因为它可以告诉你框架是如何扩展的。第一个渲染趋向于预热一堆编译迟缓的代码，当它扩展时，更大的分支可以从中受益。第二次渲染基本上是仿效页面上的代码重用是如何随着页面复杂度的增长来影响性能特征。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/19/16864f9e21cc1ae5?w=2000&h=1125&f=jpeg&s=51266)
    Addy Osmani 的 [《缺省快速:现代加载最佳实践》](https://speakerdeck.com/addyosmani/fast-by-default-modern-loading-best-practices)

12. **评估每个框架和每个依赖项**

    [并不是每个项目都需要一个框架](https://twitter.com/jaffathecake/status/923805333268639744)，[也不是单页面应用程序中的每个页面都需要加载一个框架](https://medium.com/dev-channel/a-netflix-web-performance-case-study-c0bcde26a9d9)。在Netflix的例子中，删除 React，来自客户端的几个库和相应的应用程序代码将 JavaScript 总量减少了至少 200Kb，从而使 [Netflix](https://news.ycombinator.com/item?id=15567657) 注销主页的交互时间交互时间 [缩短了50％以上](https://news.ycombinator.com/item?id=15567657) 。然后，团队利用用户在登录页面上花费的时间，对用户可能登录的后续页面进行预取 React ([详细信息请点击这里](https://jakearchibald.com/2017/netflix-and-react/))。
    
    事实上，某些项目可以 [完全移除某些框架](https://twitter.com/jaffathecake/status/925320026411950080) 并[从中受益](https://twitter.com/jaffathecake/status/925320026411950080)。一旦选择了一个框架，你最少会使用好几年。所以，如果你需要使用它，确保你的选择是经过 [深思熟虑](https://medium.com/@ZombieCodeKill/choosing-a-javascript-framework-535745d0ab90#.2op7rjakk) 的并且 [对其完全了解](https://www.youtube.com/watch?v=6I_GwgoGm1w)。
    
    Inian Parameshwaran [测量了前50个框架的性能足迹](https://youtu.be/wVY3-acLIoI?t=699) (针对 [First Contentful Paint](https://developers.google.com/web/tools/lighthouse/audits/first-contentful-paint)--从导航到浏览器从DOM渲染第一部分内容的时间)。Inian 发现，在野外，Vue 和 Preact 在桌面和移动端都是最快的，其次是 React ([幻灯片](https://drive.google.com/file/d/1CoCQP7qyvkSQ4VG9L_PTWD5AF9wF28XT/view))。您可以检查您的候选框架和建议的体系结构，并研究大多数解决方案的执行情况，例如服务器端呈现或客户端呈现。
    
    基准性能成本问题。根据 [Ankur Sethi的](https://blog.uncommon.is/the-baseline-costs-of-javascript-frameworks-f768e2865d4a) 一项 [研究](https://blog.uncommon.is/the-baseline-costs-of-javascript-frameworks-f768e2865d4a)，**无论你对它的优化程度如何，你的 React 应用程序在印度普通手机上的加载速度绝不会超过 1.1s。你的 Angular 应用程序总是需要至少 2.7s 才能启动。您的Vue应用程序的用户需要等待至少 1s 才能开始使用它。尽管您可能不会将印度定位为主要市场，但如果一个用户在网络状况不佳的情况访问您的网站应该也会呈现出相同的体验。当然，您的项目团队可以牺牲基准性能换来可维护性和开发人员效率，但是你要确保这个决定是你经过了深思熟虑之后才做的决定。
    
    您可以通过监测特性、可访问性、稳定性、性能、包生态系统、社区、学习曲线、文档、工具、跟踪记录、团队、兼容性、安全性等来评估 Sacha Greif 的 [12分制评分系统](https://medium.freecodecamp.org/the-12-things-you-need-to-consider-when-evaluating-any-new-javascript-library-3908c4ed3f49) 上的框架（或任何 JavaScript 库）。在进行选择前，至少要考虑总大小的成本 + 初始解析时间：轻量级的选项像 Preact，Inferno，Vue，Svelte或者Polymer都做得很好。框架的大小基线将为你的应用程序代码定义约束条件。
    
    一个很好的起点是为您的应用程序选择一个好的默认堆栈。[Gatsby.js](http://gatsbyjs.org/)（React），[Preact CLI](https://github.com/developit/preact-cli) 和 [PWA Starter Kit](https://github.com/Polymer/pwa-starter-kit) 为平均移动硬件上的快速加载提供了合理的默认值。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/19/1686510ba90edbcd?w=2000&h=1092&f=png&s=88714)
    图片来源：[Addy Osmani](https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4)

13. **考虑使用PRPL模式和app shell架构**

    不同的框架会对性能产生不同的影响，并且需要不同的优化策略。因此，您必须清楚地了解您所依赖的框架的所有细节。在创建一个 web 应用程序时，请参考 [PRPL模式](https://developers.google.com/web/fundamentals/performance/prpl-pattern/) 和 [应用程序 shell 体系结构](https://developers.google.com/web/updates/2015/11/app-shell)。这个想法很简单: 用最少的代码来将初始路由的交互快速呈现，然后使用 service worker 进行缓存和预缓存资源，然后使用懒加载异步加载所需的路由。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/19/1686513896797e97?w=2000&h=1078&f=png&s=69433)
    [PRPL](https://developers.google.com/web/fundamentals/performance/prpl-pattern/) 代表按需推送关键资源，渲染初始路由，预缓存剩余路由和延迟加载剩余路由。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/19/1686513e9a920831?w=2000&h=1477&f=jpeg&s=154465)
    [应用程序 shell](https://developers.google.com/web/updates/2015/11/app-shell) 是最小的 HTML，CSS 和 JavaScript 驱动的用户界面。

14. **优化 API 的性能**

    api是应用程序通过所谓的端点向内部和第三方应用程序公开数据的通信通道。在 [设计和构建API时](https://www.smashingmagazine.com/2012/10/designing-javascript-apis-usability/)，我们需要一个合理的协议来支持服务器和第三方请求之间的通信。具象状态传输(Representational State Transfer, REST)是一种完善的、合乎逻辑的选择:它定义了一组约束，开发人员可以遵循这些约束以一种高性能、可靠和可伸缩的方式访问内容。符合REST约束的Web服务称为RESTful Web服务。
    
    与好的HTTP请求一样，当从API检索数据时，服务器响应中的任何延迟都将传播到最终用户，从而延迟呈现。当资源想从API检索一些数据时，它需要从相应的端点请求数据。呈现来自多个资源的数据的组件(例如每篇评论中都有注释和作者照片的文章)可能需要多次往返服务器才能呈现所有数据。此外，通过REST返回的数据量常常超过呈现该组件所需的数据量。
    
    如果许多资源需要来自API的数据，那么API可能会成为性能瓶颈。GraphQL为这些问题提供了一个性能解决方案。就其本身而言，GraphQL是API的查询语言，也是服务器端运行时，用于通过使用为数据定义的类型系统执行查询。与REST不同的是，GraphQL可以在单个请求中检索所有数据，而响应正是所需的，不需要像REST那样获取过多或不足的数据。
    
    此外,由于GraphQL使用模式(告诉如何结构化数据的元数据),它已经可以组织数据为首选的结构,所以,例如,GraphQL,我们可以将JavaScript代码用于处理状态管理,清洁生产在客户端应用程序代码运行更快。
    
    如果您想开始学习GraphQL, Eric Baer在您的really Smashing杂志上发表了两篇精彩的文章:GraphQL入门:为什么我们需要一种新的API; GraphQL入门:API设计的发展(感谢您的提示，Leonardo!)
    
    ![](https://user-gold-cdn.xitu.io/2019/1/19/1686515d87240f2c?w=2000&h=1766&f=jpeg&s=137381)
    REST 和 GraphQL 之间的区别，通过左侧的 Redux + REST 之间的对话，右侧的 Apollo + GraphQL 进行说明。（图片来自：[Hacker Noon](https://hackernoon.com/how-graphql-replaces-redux-3fff8289221d)）

15. **您是使用 AMP 还是 Instant Articles**

    根据组织的优先级和策略，您可以考虑使用谷歌的 [AMP](https://www.ampproject.org/) 、Facebook 的 [Instant Articles](https://instantarticles.fb.com/) 或苹果的 [Apple News](https://www.apple.com/news/)。如果不使用它们，你也可以实现很好的性能，但是 AMP 确实提供了一个免费的内容分发网络（CDN）的性能框架，而 Instant Articles 将提高你在 Facebook 上的可见性和性能。
    
    对于用户而言，这些技术主要的优势是确保性能，所以有时他们更喜欢 AMP-/Apple News/Instant Pages 链接，而不是 **常规** 和潜在的臃肿页面。对于那些以内容为主的网站，主要处理很多第三方法内容，这些选择极大地加速渲染的时间。
    
    [除非他们不这样做](https://timkadlec.com/remembers/2018-03-19-how-fast-is-amp-really/)。例如，根据 Tim Kadlec 的说法，**AMP文档往往比同行更快，但并不一定意味着页面具有高性能；从性能角度来看，AMP并不是造成最大差异的因素**。
    
    对于站长而言，这些样式在各个平台可发现性并且 [增强在搜索引擎中的可见性](https://ethanmarcotte.com/wrote/ampersand/)。你也可以重新使用 AMP 作为你的 PWA 数据源来构建 [渐进式 Web AMPs](https://www.smashingmagazine.com/2016/12/progressive-web-amps/)。有什么缺点呢？显然，在一个有围墙的区域里，开发者可以创造并维持与内容分离的单独版本，防止 Instant Articles 和 Apple News  [没有实际的URLs](https://www.w3.org/blog/TAG/2017/07/27/distributed-and-syndicated-content-whats-wrong-with-this-picture/)。（**谢谢，Addy，Jeremy**）

16. **合理使用 CDN**

    根据您拥有的动态数据量，您可以将部分内容 **外包** 给 [静态站点生成工具](https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/)，将其推送到CDN并从中提供静态版本，从而避免数据库请求。您甚至可以选择基于 CDN 的 [静态主机平台](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/)，这样就可以通过给页面添加可交互组件的方式来丰富你的页面( [JAMStack](https://jamstack.org/) )。事实上，其中一些生成器(比如 [React](https://www.gatsbyjs.org/blog/2017-09-13-why-is-gatsby-so-fast/) 上面的 [Gatsby](https://www.gatsbyjs.org/blog/2017-09-13-why-is-gatsby-so-fast/) )实际上是 [网站编译器](https://tomdale.net/2017/09/compilers-are-the-new-frameworks/)，提供了许多自动优化功能。随着编译器不断地添加优化，编译后的输出会越来越小，速度也会越来越快。
    
    请注意，CDN 也是可以托管并卸载（offload）动态内容的，所以咱们没有必要把 CDN 的服务范围限定在静态资源。（另外需要你记住的是），不管你的 CDN 是否执行内容压缩（GZip）、内容转换、HTTP/2 传输以及 ESI（一种标记语言，可以用它把网页划分为单独的可缓存的实体）等操作，我们还是需要复核上述操作的，这是因为上述操作不仅会在 CDN 的 edge 处（服务器最接近用户的地方）聚合页面中的静态以及动态内容，也还会执行其它任务。
    
    注意：根据 Patrick Meenan 和 Andy Davies 的研究，HTTP / 2 在 [许多CDN上](https://github.com/andydavies/http2-prioritization-issues#cdns--cloud-hosting-services) 被 [有效打破](https://github.com/andydavies/http2-prioritization-issues#cdns--cloud-hosting-services)，因此我们不应该对其性能提升过于乐观。

### 资源优化

17. **使用 [Brotli](https://github.com/google/brotli) 或 Zopfli 进行纯文本压缩**
    
    2015年，谷歌引入了一种新的开源无损数据格式Brotli，现在所有现代浏览器都支持这种格式。在实践中，Brotli似乎比Gzip和Deflate更有效。根据设置，压缩可能(非常)缓慢，但较慢的压缩最终将导致较高的压缩率。不过，它的解压速度很快。您还可以估算站点的Brotli压缩节省。

    只有当用户通过HTTPS访问网站时，浏览器才会接受它。问题是什么?现在，有些服务器上还没有预装Brotli，如果没有自编译Nginx，就很难进行设置。尽管如此，这并不难，而且它的支持即将到来，例如，从Apache 2.4.26开始就可以使用它了。Brotli得到了广泛的支持，许多CDNs支持它(Akamai、AWS、KeyCDN、Fastly、Cloudlare、CDN77)，您甚至可以在还不支持它的CDNs上启用Brotli(with a service worker)。
    
    在最高的压缩级别上，Brotli的速度非常慢，以至于在等待动态压缩资产时，服务器开始发送响应所需的时间会抵消文件大小的任何潜在收益。但是，对于静态压缩，首选更高的压缩设置。
    
    或者，您可以考虑使用Zopfli的压缩算法，该算法将数据编码为Deflate、Gzip和Zlib格式。任何常规gzip压缩的资源都将受益于Zopfli改进的Deflate编码，因为文件将比Zlib的最大压缩小3 - 8%。问题是，文件的压缩时间要长80倍左右。这就是为什么在变化不大的资源上使用Zopfli是一个好主意，这些资源的文件设计为压缩一次并下载多次。
    
    如果您可以绕过动态压缩静态资产的成本，那么这种努力是值得的。Brotli和Zopfli都可以用于任何纯文本负载—HTML、CSS、SVG、JavaScript等等。
    
    这一战略?使用最高级别的Brotli+Gzip预压缩静态资产，使用1-4级的Brotli动态压缩(动态)HTML。确保服务器正确处理Brotli或gzip的内容协商。如果您无法在服务器上安装/维护Brotli，请使用Zopfli。

18. **使用 [响应式图像](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/) 和 [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/)**

    尽可能使用带有srcset、size和元素的响应图像。在此过程中，您还可以使用WebP格式(在Chrome、Opera、Firefox 65、Edge 18中受支持)，方法是为WebP图像提供元素和JPEG回退(参见Andreas Bovens的代码片段)，或者使用内容协商(使用Accept header)。Ire Aderinokun也有一个关于将图像转换为WebP的非常详细的教程。
    
    Sketch天生支持WebP，可以使用Photoshop的WebP插件从Photoshop导出WebP图像。还有其他选择。如果您使用WordPress或Joomla，有一些扩展可以帮助您轻松实现对WebP的支持，例如Optimus和Cache Enabler支持WordPress和Joomla自己支持的扩展(通过Cody Arsenault)。
    
    需要注意的是，虽然与等效的Guetzli和Zopfli相比，WebP图像文件的大小不支持像JPEG那样的渐进式呈现，这就是为什么用户在使用良好的旧JPEG时会更快地看到实际图像，尽管WebP图像可能在网络中更快。使用JPEG，我们可以用一半甚至四分之一的数据提供“良好”的用户体验，然后再加载其余数据，而不是像WebP那样使用半空的图像。您的决定将取决于您的目标:使用WebP，您将减少负载，使用JPEG，您将提高感知性能。
    
    在Smashing Magazine上，我们使用后缀—选择图像名称—例如brotli-compression-opt.png;每当一个映像包含这个后缀时，团队中的每个人都知道这个映像已经被优化了。还有——无耻的塞子!-杰里米·瓦格纳甚至在WebP上出版了一本很棒的书。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866e7b0a19d994?w=1600&h=915&f=jpeg&s=136508)
    响应式图像断点生成器自动生成图像和标记。

19. **图像是否恰当优化**

    当你工作在一个着陆页,这是很重要的一个方面,一个特定的图像加载快得多,确保jpeg是进步和压缩mozJPEG(改善开始呈现时间通过操纵扫描水平)或Guetzli,谷歌的新开源编码器关注感知性能,利用知识从Zopfli和WebP。唯一的缺点是:处理速度慢(每百万像素一分钟的CPU)。对于PNG，我们可以使用Pingo，对于SVG，我们可以使用SVGO或SVGOMG。如果您需要快速预览和复制或从网站下载所有SVG资产，SVG -grabber也可以为您做到这一点。
    
    每一篇关于图像优化的文章都会提到这一点，但是保持向量资产的整洁和紧凑总是值得提醒的。确保清理未使用的资产，删除不必要的元数据，并减少美术作品(以及SVG代码)中的路径点数量。(谢谢,Jeremy!)
    
    不过还有更高级的选项。你可以:
    
    - 使用Squoosh在最佳压缩级别(有损或无损)压缩、调整和操作图像，
    - 使用响应式图像断点生成器或Cloudinary或Imgix等服务来自动化图像优化。而且，在许多情况下，单独使用srcset和size将获得显著的好处。
    - 要检查响应标记的效率，可以使用image 
    - heap，这是一种命令行工具，用于测量视图大小和设备像素比之间的效率。
    - 延迟加载图像和具有lazysize的iframes，这是一个库，用于检测通过用户交互(或IntersectionObserver，我们将在后面讨论)触发的任何可见性更改。
    - 注意那些默认加载但可能永远不会显示的图像——例如在旋转木马、手风琴和图像库中。
    - 考虑使用size属性交换图像，根据媒体查询指定不同的图像显示尺寸，例如在放大镜组件中操作大小来交换源。
    - 检查图像下载的不一致性，以防止对前景和背景图像的意外下载。
    - 为了优化内部存储，你可以使用Dropbox新的Lepton格式，平均将jpeg压缩22%。
    - 注意CSS中的纵横比属性和内部尺寸属性，它们允许我们为图像设置纵横比和尺寸，因此浏览器可以提前预留一个预定义的布局槽，以避免在页面加载期间出现布局跳转。
    - 如果你有冒险精神，你可以使用Edge worker(一种基于CDN的实时过滤器)来剪切和重新排列HTTP/2流，从而更快地通过网络发送图像。边缘工作者使用JavaScript流，这些流使用可以控制的块(基本上是在CDN边缘上运行的JavaScript，可以修改流响应)，因此可以控制图像的传递。对于服务人员来说，已经太迟了，因为您无法控制在线上的内容，但是对于边缘人员，它确实有效。因此，您可以在为特定的登录页面逐步保存的静态jpeg之上使用它们。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866edf3e51c32a?w=1600&h=1045&f=jpeg&s=190320)
    图像堆输出的一个示例，这是一个命令行工具，用于测量视图大小和设备像素比之间的效率。
    
    随着客户端提示的采用，响应图像的未来可能会发生巨大的变化。客户端提示是HTTP请求头字段，例如DPR、Viewport-Width、Width、Save-Data、Accept(指定图像格式首选项)等。它们应该告知服务器关于用户浏览器、屏幕、连接等的详细信息。因此，服务器可以决定如何用适当大小的图像填充布局，并仅以所需格式提供这些图像。通过客户机提示，我们将资源选择从HTML标记转移到客户机和服务器之间的请求-响应协商。
    
    正如Ilya Grigorik所指出的，客户提示完成了图像——它们不是响应图像的替代方案。元素的作用是:在HTML标记中提供必要的艺术方向控制。客户端提示为生成的图像请求提供注释，从而支持资源选择自动化。Service Worker在客户机上提供完整的请求和响应管理功能。服务工作,例如,添加新客户提示请求标头值,重写URL和点图像请求CDN,适应响应基于连通性和用户首选项,等。它不仅适用的图像资产,但几乎所有其他请求。
    
    对于支持客户端提示的客户端，可以在图像上节省42%的字节，在70%以上的百分比上节省1MB以上的字节。在Smashing Magazine上，我们也可以测量19-32%的改进。不幸的是，客户端提示仍然需要获得一些浏览器支持。Firefox正在考虑中。但是，如果您同时为客户端提示提供正常的响应图像标记和标记，那么浏览器将评估响应图像标记并使用客户端提示HTTP头请求适当的图像源。
    
    不够好吗?您还可以使用多背景图像技术提高图像的感知性能。请记住，使用对比度和模糊不必要的细节(或删除颜色)也可以减少文件大小。啊，你需要在不影响质量的情况下放大一张小照片吗?考虑使用Letsenhance.io。
    
    到目前为止，这些优化只覆盖了基础。Addy Osmani已经发布了一份非常详细的关于基本图像优化的指南，其中深入介绍了图像压缩和颜色管理的细节。例如，您可以模糊掉图像中不必要的部分(通过对它们应用高斯模糊过滤器)以减小文件大小，最终您甚至可以开始删除颜色或将图像变为黑白，以进一步减小大小。对于背景图片，从Photoshop导出0 - 10%质量的图片也完全可以接受。啊，不要在web上使用JPEG-XR——“在CPU上解码JPEG-XRs软件端的处理无效，甚至超过了字节大小节省的潜在积极影响，尤其是在SPAs的上下文中”。
    
20. **视频是否已恰当优化**

    到目前为止，我们已经报道了一些图片，但是我们一直避免谈论一些好的动图。坦率地说，与其加载影响渲染性能和带宽的大量动画GIF，不如切换到动画WebP (GIF是一种替代)或者用循环HTML5视频来替换它们。是的，浏览器处理视频的速度很慢，而且与图像不同的是，浏览器不预装视频内容，但它们往往比gif更轻、更小。不是一个选择吗?至少我们可以用有损GIF GIF GIF giflossy来给GIF添加有损压缩。
    
    早期测试表明,内联视频在img标记显示快20×7×和解码速度比GIF等价的,除了一小部分在文件大小。虽然支持mp4">已经登陆Safari技术预览版，我们离它被广泛采用还很远，因为它不会很快闪烁。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866f5461954044?w=1600&h=900&f=jpeg&s=139705)
    Addy Osmani建议用循环的内联视频来替换动画gif。文件大小的差异很明显(节省了80%)。
    
    然而，在这片充满好消息的土地上，视频格式多年来一直在大规模发展。很长一段时间以来，我们一直希望WebM能够成为规范所有这些格式的格式，而WebP(基本上是WebM视频容器中的一个静态图像)将成为过时的图像格式的替代品。但是，尽管WebP和WebM这些天获得了支持，但是突破并没有发生。
    
    2018年，开放媒体联盟(Alliance of Open Media)发布了一种很有前途的新视频格式AV1。AV1的压缩类似于H.265编解码器(H.264的演变)，但与后者不同的是，AV1是免费的。H.265的许可定价促使浏览器厂商转而采用性能相当的AV1: AV1(就像H.265)的压缩效果是WebP的两倍。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866f6b817d2068?w=2560&h=1421&f=png&s=84729)
    AV1很有可能成为网络视频的终极标准。(图片来源:Wikimedia.org)
    
    事实上，苹果目前使用的是HEIF格式和HEVC (H.265)，最新iOS上的所有照片和视频都保存在这些格式中，而不是JPEG格式。虽然HEIF和HEVC (H.265)还没有完全公开到web上(还没有?)因此，在视频标记中添加AV1源代码是合理的，因为所有的浏览器供应商似乎都在使用它。
    
    现在,使用最广泛的和支持的编码是h,由MP4文件,在服务于文件之前,确保你的MP4 multipass-encoding处理,模糊与frei0r iirblur效应(如适用)和原子moov元数据是搬到的头文件,在您的服务器接受字节。Boris Schapira为FFmpeg提供了精确的指令来最大限度地优化视频。当然，提供WebM格式作为替代也会有所帮助。
    
    视频播放性能本身就是一个故事，如果您想深入了解它的细节，请阅读Doug Sillar关于视频和视频交付的当前状态的系列文章，其中包括关于视频交付度量、视频预加载、压缩和流媒体的详细信息。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866f8a3ffc0a36?w=1600&h=974&f=png&s=38483)
    Zach Leatherman的字体加载策略综合指南为更好的web字体交付提供了12种选择。
    
21. **Web 字体已恰当优化**

    第一个值得问的问题是，你是否能够从一开始就使用UI系统字体。如果不是这样，那么您提供的web字体很有可能包含没有使用的符号、额外的特性和权重。您可以要求类型铸造厂对web字体进行子集，或者如果您使用开源字体，可以使用Glyphhanger或Fontsquirrel对其进行子集。您甚至可以使用Peter Muller的subfont自动化整个工作流，这是一个命令行工具，它静态地分析您的页面，以生成最优的web字体子集，然后将它们注入到您的页面中。
    
    WOFF2支持非常好，对于不支持WOFF的浏览器，您可以使用WOFF作为后备——毕竟，使用系统字体可以很好地服务于遗留浏览器。web字体加载有许多、许多、许多选项，您可以从Zach Leatherman的“字体加载策略综合指南”(代码片段也可以作为web字体加载菜谱)中选择一种策略。
    
    也许现在更好的选择是使用预加载和“折衷”方法的关键FOFT。它们都使用两个阶段的呈现来分步骤交付web字体——首先是使用web字体快速准确地呈现页面所需的小超子集，然后加载家族的其他异步。不同的是，“折衷”技术只在不支持字体加载事件的情况下异步加载polyfill，因此您不需要在默认情况下加载polyfill。需要速战速决吗?Zach Leatherman有一个23分钟的快速教程和案例研究，以使您的字体秩序。
    
    通常，使用预加载资源提示来预加载字体是一个好主意，但是在您的标记中包括链接到关键CSS和JavaScript之后的提示。否则，字体加载将在第一次呈现时造成损失。不过，有选择地选择最重要的文件可能是一个好主意，比如那些对渲染至关重要的文件，或者那些可以帮助您避免可见和破坏性文本回流的文件。一般来说，Zach建议预加载每个系列的一到两种字体——如果字体不是很重要，延迟加载也是有意义的。
    
    没有人喜欢等待显示内容。使用font-display CSS描述符，我们可以控制字体加载行为，并使内容立即可读(font-display: optional)或几乎立即可读(font-display: swap)。但是，如果您希望避免文本回流，我们仍然需要使用字体加载API，特别是用于分组重绘，或者在使用第三方主机时。当然，除非您可以在Cloudflare工作人员中使用谷歌字体。谈论谷歌字体:考虑使用Google -webfonts-helper，这是一种自托管谷歌字体的简便方法。如果可以的话，总是自托管字体以获得最大限度的控制。
    
    通常，如果您使用font-display: optional，那么也使用preload可能不是一个好主意，因为它会提前触发web字体请求(如果您需要获取其他关键路径资源，则会导致网络拥塞)。对于更快的跨源字体请求，请使用preconnect，但要小心使用preload，因为预加载来自不同源的字体会引起网络争用。所有这些技术都包含在Zach的Web字体加载菜谱中。
    
    此外，如果用户在可访问性首选项中启用了Reduce Motion，或者选择了Data Saver模式(请参见Save-Data header)，那么最好选择不使用web字体(或至少不使用第二阶段呈现)。或者当用户连接速度较慢时(通过网络信息API)。
    
    要度量web字体加载性能，请考虑所有文本可见性指标(所有字体已加载且所有内容以web字体显示的时刻)，以及第一次呈现后的web字体回流计数。显然，两个指标越低，性能越好。需要注意的是，可变字体可能需要考虑显著的性能。它们为设计人员提供了更广阔的设计空间来选择字体，但代价是单个串行请求的开销，而不是多个单独的文件请求。单个请求可能会缓慢地阻塞页面上的整个排版外观。但好的一面是，有了可变字体，默认情况下我们将只获得一个reflow，因此不需要JavaScript对重新绘制进行分组。
    
    那么，什么是防弹的web字体加载策略呢?子集字体并为两阶段呈现做好准备，使用字体显示描述符声明它们，使用字体加载API对重新绘制的字体进行分组，并将字体存储在持久服务工作人员的缓存中。如果需要，您可以使用Bram Stein的字体外观观察器。如果您对测量字体加载的性能感兴趣，Andreas Marschke将研究使用字体API和UserTiming API的性能跟踪。
    
    最后，不要忘记包含unicode-range来将大字体分解为较小的特定于语言的字体，并使用Monica Dinculescu的字体样式匹配器来最小化布局中的不和谐变化，这是由于回退和web字体之间的大小差异造成的。

### 构建优化

22. **确定您的优先事项**

    首先最好明确的知道您在处理什么。运行所有资产的清单( `JavaScript `、图像、字体、第三方脚本、页面上的 **昂贵** 模块)，并将它们分组。定义旧版浏览器的基本核心体验（即完全可访问的核心内容），功能强大的浏览器的增强体验（即丰富的完整体验）和附加功能（不是绝对需要且可以延迟加载的资产，例如网页字体，不必要的样式，轮播脚本，视频播放器，社交媒体按钮，大图像）。不久前，我们发表了一篇关于 [改进粉碎杂志的表现](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/) 的文章，详细描述了这种方法。

23. **重新审视好的 切割芥末（`cutting-the-mustard`） 技术**

    如今，我们仍然可以使用 [切割技术](https://www.filamentgroup.com/lab/modernizing-delivery.html) 将核心体验发送到传统浏览器，并为现代浏览器提供增强的体验。该 [技术](https://snugug.com/musings/modern-cutting-the-mustard/) 的 [更新变体](https://snugug.com/musings/modern-cutting-the-mustard/) 将使用 `ES2015+ <script type="module">`。现代浏览器会将脚本解释为 `JavaScript` 模块并按预期运行它，而旧版浏览器无法识别该属性并忽略它，因为它是未知的 `HTML` 语法。一些廉价 Android 手机主要运行 Chrome 浏览器，尽管内存和CPU功能有限，但仍将 **削减芥末** 。最终，使用 [设备内存客户端提示标题](https://github.com/w3c/device-memory) ，我们将能够更可靠地定位低端设备。在编写本文时，仅在 Blink 中支持标头（通常用于 [客户端提示](https://caniuse.com/#search=client%20hints) ）。由于设备内存还有一个 [已在 Chrome 浏览器中提供](https://developers.google.com/web/updates/2017/12/device-memory) 的 `JavaScript API`  ，因此一种选择可能是基于 `API` 进行检测，并且只有在不支持时才会回归 **切割芥末** 技术

24. **解析 `JavaScript` 是昂贵的，所以保持小**

    在处理单页面应用程序 **SPA** 时，我们需要一些时间来初始化应用程序，然后才能呈现页面。您的设置将需要您的自定义解决方案，但您可以留意模块和技术，以加快初始渲染时间（在低端移动设备上，[解析和执行时间很容易高出2-5倍](https://medium.com/reloading/javascript-start-up-performance-69200f43b201) ）。

25. **使用 树形抖动（`Tree-shaking`） ，作用域提升（`Scope hoisting`）和代码分割（`Code-splitting`）来减少有效负载**

    [树形抖动](https://developers.google.com/web/fundamentals/performance/optimizing-javascript/tree-shaking/) 是一种清理构建过程的方法，通过仅包含实际用于生产的代码并消除 [Webpack](http://2ality.com/2015/12/webpack-tree-shaking.html) 中未使用的导入。通过 Webpack 和 Rollup ，我们还提供了[范围提升](https://medium.com/webpack/brief-introduction-to-scope-hoisting-in-webpack-8435084c171f)，允许两个工具检测链接可以展平的位置，并转换为一个内联函数，而不会影响代码。通过 WebPack 使用他们。 [代码拆分](https://webpack.js.org/guides/code-splitting/) 是另一个Webpack功能，它将您的代码库拆分为按需加载的 **块**。
    
26. **能否将 JavaScript 卸载到 Web Worker 中**

    随着代码库的不断增长，UI性能瓶颈将会出现，从而降低用户的体验。那是因为 [DOM操作](https://medium.com/google-developer-experts/running-fetch-in-a-web-worker-700dc33ac854) 与主线程上的 [JavaScript一起运行](https://medium.com/google-developer-experts/running-fetch-in-a-web-worker-700dc33ac854)。对于 [Web worker](https://flaviocopes.com/web-workers/)，我们可以将这些昂贵的操作移动到在不同线程上运行的后台进程。Web工作者的典型用例是 [预取数据和Progressive Web Apps](https://blog.sessionstack.com/how-javascript-works-the-building-blocks-of-web-workers-5-cases-when-you-should-use-them-a547c0757f6a) 以提前加载和存储一些数据，以便您以后可以在需要时使用它。可以考虑编译成
[WebAssembly](https://webassembly.org/) 这个最适合计算密集型 Web 应用程序。

27. **能否将 JavaScript 卸载到 WebAssembl 中**

28. **您使用的是提前编译器吗**

29. **仅将遗留代码提供给旧版浏览器**

30. **您是否在JavaScript中使用差异服务**

    由于 ES2015 在 [现代浏览器](http://kangax.github.io/compat-table/es6/) 中得到了  [非常好的支持](http://kangax.github.io/compat-table/es6/)，我们可以使用 [babel-preset-env](http://2ality.com/2017/02/babel-preset-env.html) 仅转换您所针对的现代浏览器不支持的ES2015 +功能。然后设置 [两个构建](https://gist.github.com/newyankeecodeshop/79f3e1348a09583faf62ed55b58d09d9)，一个在ES6中，一个在ES5中。如上所述，现在所有 [主流浏览器](https://caniuse.com/#feat=es6-module) 都 [支持](https://caniuse.com/#feat=es6-module) JavaScript 模块，因此使用 [usescript type="module"](https://developers.google.com/web/fundamentals/primers/modules) 来让支持ES模块的浏览器加载文件，而旧浏览器可以加载旧版本 `Script nomodule`。我们可以使用 [Webpack ESNext Boilerplate](https://github.com/philipwalton/webpack-esnext-boilerplate) 自动完成整个过程。对于lodash，使用 [babel-plugin-lodash](https://github.com/lodash/babel-plugin-lodash) 它将仅加载您在源中使用的模块。您的依赖项也可能依赖于其他版本的Lodash，因此 [将通用lodash requires转换为挑选的lodash](https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/) 以避免代码重复。这可能会为您节省相当多的 JavaScript 负载。

31. **通过增量解耦识别和重写遗留代码**

    长寿项目倾向于收集灰尘和过时的代码。重新访问您的依赖项并评估重构或重写最近导致问题的遗留代码所需的时间。当然，它始终是一项重大任务，但是一旦您了解遗留代码的影响，就可以从 [增量解耦](https://githubengineering.com/removing-jquery-from-github-frontend/) 开始。首先，设置指标，跟踪遗留代码调用的比率是保持不变还是下降，而不是上升。公开阻止团队使用该库，并确保您的 CI [警告](https://github.com/dgraham/eslint-plugin-jquery) 开发人员，如果它在拉取请求中使用。[polyfills](https://githubengineering.com/removing-jquery-from-github-frontend/#polyfills) 可以帮助从遗留代码转换为使用标准浏览器功能的重写代码库。

32. **识别并删除未使用的 `CSS` / `JavaScript`**

    Chrome 浏览器中的 [CSS和JavaScript代码覆盖率](https://developers.google.com/web/updates/2017/04/devtools-release-notes#coverage) 允许您了解哪些代码已执行/已应用，哪些代码尚未执行。您可以开始记录覆盖范围，在页面上执行操作，然后浏览代码覆盖率结果。一旦检测到未使用的代码，[找到那些模块和延迟加载 `import()`](https://twitter.com/TheLarkInn/status/1012429019063578624)（参见整个线程）。然后重复覆盖配置文件并验证它现在在初始加载时发送的代码较少。您可以使用 [Puppeteer](https://github.com/GoogleChrome/puppeteer) 以编程方式收集代码覆盖率，Canary也允许您导出代码覆盖率结果。正如 Andy Davies 指出的那样，您可能希望收集现代和旧版浏览器的代码覆盖率。[Puppeteer](https://github.com/GoogleChrome/puppeteer) 还有许多 [其他用例](https://github.com/GoogleChromeLabs/puppeteer-examples)，例如：[自动视觉差异](https://meowni.ca/posts/2017-puppeteer-tests/) 或 [监视每个构建的未使用的CSS](http://blog.cowchimp.com/monitoring-unused-css-by-unleashing-the-devtools-protocol/)。

33.  **修剪 `JavaScript` 依赖项的大小**

    正如 Addy Osmani 指出的那样，当你只需要一个分数时，你很可能会发送完整的 JavaScript 库，以及不需要它们的浏览器的日期 [polyfill](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)，或者只是重复代码。为避免开销，请考虑使用 [webpack-libs-optimization](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)，在构建过程中删除未使用的方法和 [polyfill](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)。将捆绑审核添加到常规工作流程中。

34. **您是否正在使用 `JavaScript` 块的预测预取**

    我们可以使用启发式方法来决定何时预加载 JavaScript 块。[Guess.js](https://github.com/guess-js/guess) 是一组工具和库，它们使用 Google Analytics 数据来确定用户最有可能从给定页面访问哪个页面。但是需要注意的是:您可能会提示浏览器使用不需要的数据并预取不需要的页面，因此在预取请求的数量上保持相当保守是个好主意。一个好的用例是预取结帐中所需的验证脚本，或者当一个关键的号召性用语进入视口时的推测性预取。

35. **考虑微优化和 [渐进式启动](https://aerotwist.com/blog/when-everything-is-important-nothing-is/)**

    在这两种情况下，我们的目标应该是设置 [渐进式启动](https://aerotwist.com/blog/when-everything-is-important-nothing-is/)：使用服务器端渲染来获得快速的第一个有意义的绘制，但也包括一些最小的必要 JavaScript，以保持交互时间接近第一个有意义的绘制。如果 JavaScript 在 First Meaningful Paint 之后来得太晚，浏览器可能会在解析，编译和执行后期发现的 JavaScript 时[锁定主线程](https://davidea.st/articles/measuring-server-side-rendering-performance-is-tricky)，从而给 [站点或应用程序](https://philipwalton.com/articles/why-web-developers-need-to-care-about-interactivity/) 的[交互](https://philipwalton.com/articles/why-web-developers-need-to-care-about-interactivity/) 带来手铐。为了避免它，总是将函数的执行分解为单独的异步任务，并尽可能使用 `requestIdleCallback`。考虑使用 WebPack 的动态 `import()` 支持延迟加载 UI 部分，避免加载，解析和编译成本，直到用户真正需要它们。
    
35. **利用针对目标JavaScript引擎的优化**    

36. **客户端呈现或服务器端呈现**

37. **限制第三方脚本的影响**

    通过所有性能优化，我们通常无法控制来自业务需求的第三方脚本。这时候建议从自己的服务器，而不是从供应商的服务器加载第三方脚本。另一种选择是建立 **内容安全策略（CSP）** 以限制第三方脚本的影响，例如禁止下载音频或视频。最好的选择是通过嵌入脚本，`<iframe>` 以便脚本在 **iframe** 的上下文中运行，因此无法访问页面的 DOM ，也无法在您的域上运行任意代码。可以使用该 `sandbox` 属性进一步约束 `iframe` ，因此您可以禁用 `iframe` 可能执行的任何功能，例如阻止脚本运行，阻止警报，表单提交，插件，访问顶部导航等。如果要[对第三方进行压力测试](https://csswizardry.com/2017/07/performance-and-resilience-stress-testing-third-parties/)，请检查 DevTools 中性能配置文件页面中的自下而上的摘要，测试如果请求被阻止或超时的情况会发生什么 - 对于后者，您可以使用 WebPageTest 的 Blackhole 服务器 `blackhole.webpagetest.org` ，您可以将特定域指向在你的 `hosts` 文件中。

38. **正确设置 HTTP 缓存头**

    仔细检查 `expires`， `cache-control`， `max-age` 和其他 HTTP 缓存标头是否已正确设置。通常，资源应该可以在[非常短的时间内（如果它们可能更改）或无限期（如果它们是静态的）](https://jakearchibald.com/2016/caching-best-practices/) 可缓存- 您只需在需要时更改 URL 中的版本。禁用 `Last-Modified` 标头，因为任何带有它的资产都会导致带有 `If-Modified-Since-header` 的条件请求，即使资源位于缓存中也是如此。与 ... 相同 Etag 。使用 `Cache-control: immutable`，专为指纹静态资源设计，以避免重新验证（截至2018年12月，[Firefox，Edge和Safari支持](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) ；仅在 https:// 事务中支持 Firefox ）。事实上，在HTTP存档中的所有页面中， `2％` 的请求和 `30％` 的网站似乎 [包含至少1个不可变响应](https://discuss.httparchive.org/t/cache-control-immutable-a-year-later/1195)。另外，大多数使用它的网站都在具有长寿新生。而且需要注意的是，仔细检查你是不是发送不必要的报头（例如 `x-powered-by`， `pragma`， `x-ua-compatible`， `expires`和其他人）和你包括 [有用的安全和性能头](https://www.fastly.com/blog/headers-we-want) （如 `Content-Security-Policy`， `X-XSS-Protection`， `X-Content-Type-Options`等）。最后，请记住单页应用程序中 [CORS 请求](https://medium.com/@ankur_anand/the-terrible-performance-cost-of-cors-api-on-the-single-page-application-spa-6fcf71e50147) 的 [性能成本](https://medium.com/@ankur_anand/the-terrible-performance-cost-of-cors-api-on-the-single-page-application-spa-6fcf71e50147)。

### 交付优化

39. **异步加载JavaScript**

    当用户请求页面时，浏览器获取 HTML 并构造 DOM ，然后获取 CSS 并构造 CSSOM，然后通过匹配 DOM 和 CSSOM 生成渲染树。如果需要解析任何 JavaScript，浏览器将不会开始渲染页面，直到它被解析，从而延迟渲染。作为开发人员，我们必须明确告诉浏览器不要等待并开始呈现页面。对脚本执行此操作的方法是使用 HTML 中的 `defer` 和 `async` 属性。在实践中，事实证明，我们应该更喜欢使用延迟异步。根据 [Steve Souders的说法](https://youtu.be/RwSlubTBnew?t=1034)，一旦 `async` 脚本到达，它们就会被立即执行。如果这种情况发生得非常快，例如当脚本处于缓存区时，它实际上可以阻止 HTML 解析器。在 `defer` 浏览 HTML 之前，浏览器不会执行脚本。因此，除非您在开始渲染之前需要执行 JavaScript ，否则最好使用它异步。

40. **使用 [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) 延迟加载昂贵的组件**

    一般来说，延迟加载所有昂贵的组件是个好主意，例如繁重的 `JavaScript`，`video`，`iframe`，小部件和潜在的图像。最高效的方法是使用 [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)，它提供了一种异步观察目标元素与祖先元素或顶级文档视口交叉点的变化的方法。另外，请注意该 [lazyload属性](https://css-tricks.com/a-native-lazy-load-for-the-web-platform/)，这将允许我们 `iframe` 本地指定哪些图像和s应该是延迟加载的。[功能策略lazyload](https://www.chromestatus.com/feature/5641405942726656) 将提供一种机制，允许我们基于每个域强制选择加入或退出 [lazyload](https://css-tricks.com/a-native-lazy-load-for-the-web-platform/) 功能（类似于 [内容安全策略](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) 的工作方式）。
    
41. **逐步加载图像**

42. **快速推送关键 CSS**

    为了确保浏览器尽快开始渲染页面，收集开始渲染页面的第一个可见部分所需的所有 `CSS` (（称为 **关键CSS** 或 **首屏CSS** ）已成为一种 [常见做法](https://www.smashingmagazine.com/2015/08/understanding-critical-css/)）,并将其内联添加 `<head>` 到页面中，从而减少往返次数。由于在慢启动阶段交换的包的大小有限，因此关键 `CSS` 的预算约为 `14 KB`。或者，使用HTTP / 2服务器推送，但随后可能需要创建一个缓存感知的HTTP / 2服务器推送机制。

43. **尝试重新组合 CSS 规则**

    我们已经习惯了关键的 `CSS`，但是有一些优化可以超越它。哈里·罗伯茨以非常惊人的结果进行了 [一项非凡的研究](https://csswizardry.com/2018/11/css-and-network-performance/)。例如，将主 `CSS` 文件拆分为单独的媒体查询可能是个好主意。这样，浏览器将检索具有高优先级的关键 `CSS`，以及具有低优先级的所有其他 - 完全脱离关键路径。另外，请避免 `<link rel="stylesheet" />` 在 `async` 片段之前放置。如果脚本不依赖于样式表，请考虑将阻塞脚本置于阻塞样式之上。如果他们这样做，将 `JavaScript` 拆分为两个并将其加载到 `CSS` 的任一侧。

44. **流响应**

    常常被遗忘和被忽视的，[流](https://streams.spec.whatwg.org/) 的读取或写入数据的异步块，其中只有一个子集的可能是内存可在任何给定时间提供一个接口。基本上，只要第一块数据可用，它们就允许使原始请求的页面开始使用响应，并使用针对流进行优化的解析器逐步显示内容。我们可以从多个来源创建一个流。例如，您可以让服务工作者构建一个 `shell` 来自缓存，而主体来自网络，而不是提供空的 `UI shell` 并让 `JavaScript` 填充它。正如 `Jeff Posnick` 所指出的，如果您的 `Web` 应用程序由 CMS 提供服务，该服务器通过将部分模板拼接在一起来呈现 `HTML`，则该模型直接转换为使用流式响应，模板逻辑在服务工作者而不是服务器中复制。Jake Archibald 的 [The Year of Web Streams](https://jakearchibald.com/2016/streams-ftw/) 文章重点介绍了如何构建它，性能提升非常明显。流式传输整个 `HTML` 响应的一个重要优点是，在初始导航请求期间呈现的 `HTML` 可以充分利用浏览器的流 `HTML` 解析器。在页面加载后插入到文档中的 `HTML` 块（通过 `JavaScript` 填充的内容很常见）无法利用此优化。

45. **考虑使组件连接/设备内存感知**

    数据可能很昂贵，随着负载的增加，我们需要尊重那些在访问我们的网站或应用程序时选择节省数据的用户。[保存数据客户端提示请求头](https://developers.google.com/web/updates/2016/02/save-data) 允许我们定制应用程序和负载，以限制成本和性能的用户。实际上，您可以 [将对高DPI图像的请求重写为低DPI图像](https://css-tricks.com/help-users-save-data/)，删除 web 字体、奇特的视差效果、预览缩略图和无限滚动、关闭视频自动播放、服务器推送、减少显示项的数量和降低图像质量，甚至更改交付标记的方式。此外，您还可以使用 [网络信息API](https://googlechrome.github.io/samples/network-information/) 根据网络类型交付低/高分辨率的图像和视频。[网络信息API](https://googlechrome.github.io/samples/network-information/) 和特异性 `navigator.connection.effectiveType`（ 铬62+ ）使用 `RTT`，下行，网络类型值（和一些其他）来提供的连接，以及用户可以处理数据的表示。

46. **考虑使您的组件设备具有内存感知能力**

47. **预热连接以加快传输速度**

    使用资源提示节省时间 [dns-prefetch](https://caniuse.com/#search=dns-prefetch)（在后台执行DNS查找），[preconnect](https://www.caniuse.com/#search=preconnect) （要求浏览器在后台启动连接握手（DNS，TCP，TLS）），[prefetch](https://caniuse.com/#search=prefetch) （要求浏览器请求资源）和 [preload](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)（除了其他东西之外，它预取资源而不执行它们）。注意：如果你正在使用 `preload`，`as` 必须定义或没有加载，预加载的字体没有 `crossorigin` 属性将双倍获取。

48. **使用 Service workers 进行缓存和网络回退**

    如果您的网站是通过 HTTPS 运行的，请使用 **[实用主义者服务工作者指南](https://github.com/lyzadanger/pragmatist-service-worker)** 将静态资产缓存在服务工作者缓存中并存储脱机回退（甚至是脱机页面）并从用户的计算机中检索它们，而不是转到网络。通常，一个常见的可靠策略是将 `app shell` 与一些关键页面一起存储在服务工作者的缓存中，例如离线页面，首页以及在您的案例中可能很重要的任何其他内容。如果您正在构建一个渐进式 Web 应用程序，并且当您的服务工作者缓存从 CDN 提供的静态资产时遇到膨胀的缓存存储，请确保对于跨源资源存在正确的CORS响应头，您不会缓存不透明的响应与您的服务工作者无意中，您通过将属性添加到标记来选择跨源图像资产进入 CORS 模式。`crossorigin<img>` 使用服务工作者的一个很好的起点是 [Workbox](https://developers.google.com/web/tools/workbox/)，这是一组专门为构建渐进式 Web 应用程序而构建的服务工作者库。

49. **您是否使用 CDN / Edge 上的 Service workers（例如，进行A / B测试）**

    此时，我们已经非常习惯在客户端上运行服务工作者，但是有了 [CDN在服务器上实现它们](https://blog.cloudflare.com/introducing-cloudflare-workers/)，我们也可以使用它们来调整边缘性能。例如，在 A / B 测试中，当 HTML 需要为不同用户改变其内容时，我们可以 [使用CDN服务器上的Service Workers](https://www.filamentgroup.com/lab/servers-workers.html) 来处理逻辑。我们还可以对 [HTML重写](https://twitter.com/patmeenan/status/1065567680298663937) 进行 [流式处理](https://twitter.com/patmeenan/status/1065567680298663937)，以加快使用Google字体的网站的速度。

50. **您是否优化了渲染性能**

    使用 [CSS包含隔离昂贵的组件](https://caniuse.com/#search=contain) -- 例如，限制浏览器样式的范围，限制画布外导航或第三方窗口小部件的布局和绘制工作。滚动页面或元素设置动画时确保没有延迟，并且您每秒都要达到 60 帧。如果这是不可能的，那么至少使每秒帧数保持一致优于 60 到 15 的混合范围。使用 CSS 的  [will-change](https://caniuse.com/#feat=will-change) 告知浏览器哪些元素和属性将改变。

51. **您是否优化了渲染体验**

    虽然组件在页面上的显示顺序以及我们如何为浏览器提供资产的策略很重要，但我们也不应低估[感知性能](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/) 的作用。在加载资产时，我们可以尝试始终领先客户一步，因此在后台发生相当多的事情时，体验会很快。为了让客户保持参与，我们可以测试 [骨架屏幕](https://twitter.com/lukew/status/665288063195594752) （实施演示）而不是加载指标，添加过渡/动画，并且在没有更多优化的情况下基本上 [欺骗用户体验](https://blog.stephaniewalter.fr/en/cheating-ux-perceived-performance-and-user-experience/)。请注意：在部署之前应该测试骨架屏幕，因为一些测试显示骨架屏幕可以通过所有指标执行最差。

### HTTP/2

52. **迁移到HTTPS，然后打开HTTP / 2**

    随着 [Google 向更安全的网络发展](https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html)，并最终将 Chrome 中的所有 HTTP 网页认定为 **不安全**的大环境下，迁移到 [HTTP / 2环境](https://http2.github.io/faq/) 是不可避免的。[HTTP / 2 从目前来看得到很好的支持](https://caniuse.com/#search=http2)， 而且，在大多数场景下，使用 HTTP/2 会让你大力出奇。一旦在 HTTPS 上运行，您可以在 service workers 和 server push 方面得到 [显著的性能提升](https://www.youtube.com/watch?v=RWLzUnESylc&t=1s&list=PLNYkxOF6rcIBTs2KPy1E6tIYaWoFcG3uj&index=25)。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/19/16861b2abdae1a8e?w=1600&h=776&f=png&s=53729)
    最终，谷歌计划将所有 HTTP 页面标记为不安全的，并将有问题的 HTTPS 的 HTTP 安全指示器更改为红色三角形。
    
    最耗时的任务是 [迁移到 HTTPS](https://https.cio.gov/faq/)，不过这取决于你的 HTTP/1.1 用户基础有多大（即使用旧版操作系统或浏览器的用户），你将不得不为旧版的浏览器性能优化发送不同的构建版本，这需要你采用 [不同的构建流程](https://rmurphey.com/blog/2015/11/25/building-for-http2)。注意：开始迁移和新的构建过程可能会很棘手，而且耗费时间。接下来所讲的内容，都是针对之前切过 HTTP/2 环境或者现在正准备切 HTTP/2 环境（的读者）来展开的。

53. **正确部署HTTP / 2**

    再次强调一下，需要对现阶段正如何提供在你开始使用 HTTP/2 请求资源之前，需要搞清楚你以前是如何请求资源的。另外需要你在载入大模块以及并行载入小模块之间找到一个平衡点。最终，仍然是 [最好的请求就是没有请求](http://alistapart.com/article/the-best-request-is-no-request-revisited)，然而我们的目标是在快速传输资源和缓存之间找到一个好的平衡点。。
    
    一方面，你可能想要避免合并所有资源，而是把整个界面分解成许多小模块，然后在构建过程中压缩这些小模块，最后通过 [scount approach 的方法](https://rmurphey.com/blog/2015/11/25/building-for-http2) 引用和并行加载这些小模块。这样的话，一个文件的更改就不需要重新下载整个样式表或  JavaScript。这样还可以 [最小化解析时间](https://css-tricks.com/musings-on-http2-and-bundling/)，并将单个页面的负荷保持在较低的水平。
    
    另一方面，[打包仍然很重要](http://engineering.khanacademy.org/posts/js-packaging-http2.htm)。首先， **压缩将让你受益**。在压缩大文件的过程中，借助目录重用的特点，达到优化性能的目的，而小的单独的文件则不会。有标准的工作来解决这个问题，但现在还远远不够。其次，浏览器还 **没有为这种工作流优化**。例如，Chrome 将触发 [进程间通信](https://www.chromium.org/developers/design-documents/inter-process-communication)（IPCs），与资源的数量成线性关系，因此页面中如果包含数以百计的资源将会造成浏览器性能损失。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/18/1686198912a14bb4?w=1600&h=1162&f=jpeg&s=62258)
    要想能达到 HTTP/2 的最佳使用效果，可以考虑使用 [渐进加载CSS](https://jakearchibald.com/2016/link-in-body/), Chrome 的 Jake Archibald 建议我们这样做。
    
    你可以尝试 [渐进加载 CSS](https://jakearchibald.com/2016/link-in-body/)。事实上，由于 Chrome 69 版本，内部 CSS [不再阻止 Chrome 渲染](https://twitter.com/patmeenan/status/1037027969842208777)。显然，这种做法不利于 HTTP / 1.1 用户，所以你可能需要针对不同的浏览器创建并发送该浏览器支持的 HTTP 协议报头，这还只是部署过程中稍微复杂的地方。你可以使用 [HTTP/2 的 connection coalescing](https://daniel.haxx.se/blog/2016/08/18/http2-connection-coalescing/)，可以让你在 HTTP/2 环境使用域名共享）来避开这些，但在实践中实现这一目标是很困难的。
    
    怎么做呢？如果你运行在 HTTP/2 之上，发送6-10 个包是个理想的折中（对旧版浏览器也不会太差）。对于你自己的网站，你可以通过实验和测量来找到最佳的平衡点。

54. **您的服务器和 CDN 是否支持 HTTP / 2**

    不同的服务器和 CDN 可能会以不同的方式支持 HTTP / 2。快速使用  [TLS](https://istlsfastyet.com/) 检查您的选项，或快速查找服务器的性能，或者您希望看到可以支持的特性。
    
    参考 Pat Meenan 对 [HTTP / 2优先级](https://blog.cloudflare.com/http-2-prioritization-with-nginx/) 和 [测试服务器支持HTTP / 2优先级](https://github.com/pmeenan/http2priorities) 的的研究。根据 Pat 的说法，建议启用 BBR 拥塞控制并将其设置 `tcp_notsent_lowat` 为 16KB 以进行 HTTP / 2 优先级排序，以便在 Linux 4.9 内核及更高版本上可靠地运行（感谢Yoav！）。Andy Davies对跨浏览器，[CDN和云托管服务的 HTTP / 2优先级](https://github.com/andydavies/http2-prioritization-issues#cdns--cloud-hosting-services) 进行了类似的研究。

![](https://user-gold-cdn.xitu.io/2019/1/18/1686190e8bb09824?w=1600&h=1169&f=png&s=86573)
[TLS还快吗](https://istlsfastyet.com/)?允许您在切换到HTTP/2时检查服务器和CDNs选项。

55. **是否启用了 OCSP stapling**

    通过 [在您的服务器上启用 OCSP stapling](https://www.digicert.com/enabling-ocsp-stapling.htm)，可以加快 TLS 握手速度。在线证书状态协议（OCSP）作为证书撤销列表（CRL）协议的替代方案。两种协议都用于检查 SSL 证书是否已被撤销。但是，OCSP 协议不要求浏览器花时间下载然后在列表中搜索证书信息，因此减少握手所需要的时间。

56. **是否采用 IPv6**

    由于我们的 [IPv4空间不足](https://en.wikipedia.org/wiki/IPv4_address_exhaustion)，而主要移动网络正在迅速采用 IPv6（美国已经达到了 50％ 的 IPv6 采用率阈值），因此最好 [将DNS更新为IPv6](https://blog.paessler.com/ask-the-expert-current-status-on-ipv6) 以保证未来的防范。只需确保通过网络提供双栈支持 - 它允许 IPv6 和 IPv4 同时并行运行。毕竟，IPv6 不是向后兼容的。此外，有 [研究表明](https://www.cloudflare.com/ipv6/)，正是因为 IPv6 自带 NDP 以及路由优化，所以才能够让网站的载入速度提升 10% 到 15%。

57. **是否正在使用 HPACK 压缩**

    如果您使用的是 HTTP / 2，请仔细检查您的服务器是否为 HTTP 响应标头 [实施HPACK压缩](https://blog.cloudflare.com/hpack-the-silent-killer-feature-of-http-2/)，以减少不必要的开销。由于 HTTP / 2 服务器相对较新，它们可能不完全支持规范，就比如 HPACK。[H2spec](https://github.com/summerwind/h2spec) 是一个用来检查的很好的工具，他[压缩算法](https://www.mnot.net/blog/2018/11/27/header_compression) 非常有效。

58. **确保服务器上的安全性是防攻击的**

    HTTP / 2 的所有浏览器实现都通过 TLS 运行，因此您可能希望页面避免出现安全警告或者是页面上的某些交互无法正常实现。这时候您需要仔细检查您的 [安全标头是否设置正确](https://securityheaders.com/)以及[证书](https://www.ssllabs.com/ssltest/)，[来消除已知漏洞](https://www.smashingmagazine.com/2016/01/eliminating-known-security-vulnerabilities-with-snyk/) 。另外，请确保通过HTTPS加载所有外部插件和跟踪脚本，无法进行跨站点脚本编写，并且网站已经正确设置了 [HTTP严格传输安全标头](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) 和 [内容安全策略标头](https://content-security-policy.com/)。

### 测试和监测

59. **您是否优化了审计和调试工作流程**

    从字面上来看这可能不是什么影响性能的大问题，但在触手可及的地方设置合适的设置可能会为给您节省大量的测试时间。可以考虑使用 Tim Kadlec 的 [WebPageTest](https://github.com/tkadlec/webpagetest-alfred-workflow) 中的 [Alfred Workflow](https://github.com/tkadlec/webpagetest-alfred-workflow) 将测试提交给 [WebPageTest](https://github.com/tkadlec/webpagetest-alfred-workflow) 的公共实例。您还可以从 [Google电子表格中驱动WebPageTest](https://calendar.perfplanet.com/2014/driving-webpagetest-from-a-google-docs-spreadsheet/) ，并将可访问性，性能和 SEO 分数纳入您使用 `Lighthouse CI` 的 `Travis` 设置或 [直接使用Webpack](https://twitter.com/addyosmani/statuses/1017655423099289600)。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/18/1686165a6d1710d6?w=1600&h=921&f=png&s=101604)
    使用 Lighthouse CI 将 [可访问性，性能和SEO分数](https://web.dev/fast/using-lighthouse-ci-to-set-a-performance-budget) 集成到 Travis 设置中，可以突出显示新功能对所有贡献开发人员的性能影响。

60. **您是否在代理浏览器和旧版浏览器中测试过**

    仅仅在 Chrome 和 Firefox 浏览器进行测试是不够的。我们还需要了解网站在代理浏览器和旧版浏览器中的工作方式。例如，UC 浏览器 和 Opera Mini ，这些浏览器 [在亚洲占有很大的市场份额](http://gs.statcounter.com/#mobile_browser-as-monthly-201511-201611) （ **高达35％** ）。测量您感兴趣的国家/地区的 [平均互联网速度](https://www.webworldwide.io/)，以避免出现重大意外情况。测试网络节流，并仿真一个高 DPI 设备。[BrowserStack](https://www.browserstack.com/)  很不错，但也要在实际设备上测试。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/18/1686163c92d7aec6?w=725&h=572&f=gif&s=817417)
    [k6](https://github.com/loadimpact/k6) 允许您编写单元测试 - 类似的性能测试。
    
61. **您是否测试了辅助功能**

    当浏览器开始加载页面时，它构建一个DOM，如果有像屏幕阅读器这样的辅助技术在运行，它还会创建一个可访问性树。然后屏幕阅读器会通过查询可访问性树来检索信息并使其对用户可用 —— 这有时是默认的，有时是按需的。
    
    我们所说的快速交互时间，通常指的是用户通过点击链接和按钮与页面交互的速度。当屏幕阅读器的上下文略有不同的时候，快速交互时间意味着屏幕阅读器可以在页面显示导航，到屏幕阅读器上的用户可以用键盘与页面进行交互所需的时间。
    
    莱内·沃森（LéonieWatson） 在 [易访问性性能方面](https://www.youtube.com/watch?v=n1sXj9oAXFU) 做了一次大开眼界的 [演讲]((https://www.youtube.com/watch?v=n1sXj9oAXFU))，特别是慢加载对屏幕阅读器发布延迟的影响。屏幕阅读器习惯于快节奏的公告和快速导航，因此可能这个辅助功能可能不适用于视力正常的用户。
    
    使用 JavaScript 脚本进行大页面和 DOM 操作会导致屏幕阅读器公告延迟。几乎每个平台(Jaws、NVDA、画外音、旁白、Orca)都可以使用屏幕阅读器进行一些检测和测试，这是一个相对未开发的领域。

62. **您是否建立了连续监控**

    有一个 [WebPagetest](https://www.webpagetest.org/) 私人的实例总是有利于快速和无限的测试。但是，一个带有[自动性能回归警报](https://calendar.perfplanet.com/2017/automating-web-performance-regression-alerts/)报的连续监视工具 （如 [Sitespeed](https://www.sitespeed.io/)， [Calibre](https://calibreapp.com/) 和 [SpeedCurve](https://speedcurve.com/) ） 将会给您提供更详细的性能描述。设置您自己的用户计时标记来度量和监视特定的业务度量。同时，考虑添加自动化性能回归警报来监控随着时间而发生的变化。
    
    使用 RUM 解决方案来监视性能随时间的变化。对于自动化的类单元测试的负载测试工具，您可以使用 [k6](https://github.com/loadimpact/k6) 脚本  API。此外，可以了解下[SpeedTracker](https://speedtracker.org/)，[Lighthouse](https://github.com/GoogleChrome/lighthouse) 和 [Calibre](https://calibreapp.com/)。

### 速效方案

此列表非常全面，按照这个清单完成所有优化可能需要一段时间。那么，如果你只有1小时的时间来获得重大改进，你会怎么做？让我们把这个清单归结为 **12个低挂的水果**。显然，在开始之前和完成之后，测量结果是包括在3G和电缆连接上开始渲染时间和速度指数。

1. 测量实际环境的体验并设定适当的目标。一个好的目标是：第一次有意义的绘制 < 1 s，速度指数（Speed Index） < 1250，在慢速的 3G 网络上的交互 < 5s，对于重复访问，TTI < 2s。优化渲染开始时间和交互时间。
2. 为主模板准备关键CSS，并将其包含在 `<head>` 页面中。（您的预算为14 KB）。对于CSS / JS，文件大小不超过 [170KB gzipped](https://infrequently.org/2017/10/can-you-afford-it-real-world-web-performance-budgets/)（0.7MB解压缩）。。
3. 尽可能多地减少代码量，优化，推迟和延迟加载脚本，检查轻量级备选方案并限制第三方脚本的影响。
4. 仅将遗留代码提供给旧版浏览器 `<script type="module">`。
5. 尝试重新组合CSS规则并测试体内 CSS。
6. 添加资源提示以加快交付速度，使用 `dns-lookup`，`preconnect`，`prefetch` 和 `preload`。
7. 分离 Web 字体并异步加载它们，并在 CSS 中快速使用字体显示渲染。
8. 优化图像，并考虑将 WebP 用于关键页面（例如登录页面）。
9. 检查是否正确设置了 HTTP 缓存头和安全头。
10. 在服务器上启用 `Brotli` 或 `Zopfli` 压缩。 （如果都行不通，那就用 `
Gzip` 压缩。）
11. 如果HTTP / 2可用，请启用 HPACK 压缩，并开始监视混合内容警告。启用 OCSP 装订。
12. 如果可能，在服务工作缓存中缓存诸如字体，样式，`JavaScript` 和图像之类的资源。

### 下载优化性能清单（PDF，Apple Pages）

结合这个性能优化清单，您就已经为任何类型的前端性能项目做好了准备。请随意下载该清单的打印版PDF，以及一个可编辑的苹果页面文档，以定制您需要的清单：
- [下载清单PDF](https://www.dropbox.com/s/21vof23jlwf0swc/performance-checklist-1.2.pdf?dl=0) （PDF，166 KB）
- [下载Apple Pages中的清单](https://www.dropbox.com/s/xyf5qjnp1ii5okm/performance-checklist-1.2.pages?dl=0) （.pages，275 KB）
- [下载MS Word中的清单](https://www.dropbox.com/s/76b3yzexqdwsg65/performance-checklist-1.2.docx?dl=0) （.docx，151 KB）

如果您需要替代方案，还可以查看 [Dan Rublic](https://github.com/drublic/checklist) 的 [前端性能优化清单](https://github.com/thedaviddias/Front-End-Performance-Checklist)，Jon Yablonski 的 [设计师的 Web 性能优化表](https://jonyablonski.com/designers-wpo-checklist/) 和 [FrontendChecklist](https://github.com/thedaviddias/Front-End-Performance-Checklist)。
    
### 动身吧！

某些优化可能超出了您的工作或预算范围，或者考虑到您必须处理的遗留代码，可能只是过度杀伤。没关系！使用这份性能优化清单作为一个通用（希望是全面的）指南，并创建适一个用于您自己的应用场景的问题清单。但最重要的是，在优化之前要先测试并且监测您自己的项目。最后，祝愿大家在 2019 年页面性能有大大的提升！

**非常感谢 Guy Podjarny，Yoav Weiss，Addy Osmani，Artem Denysov，Denys Mishunov，Ilya Pukhalski，
Jeremy Wagner，Colin Bendell，Mark Zeman，Patrick Meenan，Leonardo Losoviz，Andy Davies，Rachel Andrew，
Anselm Hannemann，Patrick Hamann，Andy Davies，Tim Kadlec，Rey Bango，Matthias Ott，Peter Bowyer，Phil
Walton，Mariana Peralta，Philipp Tellis，Ryan Townsend，Ingrid Bergman，Mohamed Hussain S H，Jacob
Groß，Tim Swalling，Bob Visser，Kev Adamson，Adir Amsalem，Aleksey Kulikov和Rodney Rehm对这篇文章的校对，同样也感谢我们出色的社区，分享了他们在性能优化工作中学习到的技术和经验，供大家使用。你们真正的非常了不起！**

