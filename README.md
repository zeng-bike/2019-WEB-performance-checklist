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
    
    在 2005 年，[Google推出](https://opensource.googleblog.com/2015/09/introducing-brotli-new-compression.html) 了 [Brotli](https://github.com/google/brotli)，一个新的开源无损数据压缩格式，现在已经被 [所有的现代浏览器所支持](https://caniuse.com/#search=brotli)。实际上，Brotli 比 Gzip 和 Deflate [更有效](https://quixdb.github.io/squash-benchmark/#results-table)。压缩速度可能会非常慢，但这取决于设置信息，可是缓慢的压缩过程会提高压缩率。它仍然可以快速解压缩，并且您还可以[估算您网站的Brotli压缩成本](https://tools.paulcalvano.com/compression.php)。

    只有当用户通过 HTTPS 访问网站时，浏览器才会采用。Brotli 现在还不能预装在某些服务器上，而且如果不自己构建 NGINX 和 UBUNTU 的话很难部署。[不过这也并不难](https://www.tinywp.in/nginx-brotli/)，而且它的支持即将到来，例如，[从Apache 2.4.26开始](https://httpd.apache.org/docs/trunk/mod/mod_brotli.html) 就可以使用它了。Brotli 得到了广泛的支持，许多 CDN 支持它( [Akamai](https://community.akamai.com/community/web-performance/blog/2017/08/18/brotli-support-enablement-on-akamai)、[AWS](https://medium.com/@felice.geracitano/brotli-compression-delivered-from-aws-7be5b467c2e1)、[KeyCDN](https://www.keycdn.com/blog/keycdn-brotli-support)、[Fastly](https://docs.fastly.com/guides/detailed-product-descriptions/performance-optimization-package)、[Cloudlare](https://support.cloudflare.com/hc/en-us/articles/200168396-What-will-Cloudflare-compress-)、[CDN77](https://www.cdn77.com/brotli))，您甚至可以在 [还不支持它的CDN上](https://calendar.perfplanet.com/2016/enabling-brotli-even-on-cdns-that-dont-support-it-yet/) [启用Brotli](http://calendar.perfplanet.com/2016/enabling-brotli-even-on-cdns-that-dont-support-it-yet/)(与 service worker 一起)。
    
    在最高级别的压缩下，Brotli 的速度会变得非常慢，以至于服务器在等待动态压缩资源时开始发送响应所花费的时间可能会使我们对文件大小的优化无效。但是，对于静态压缩，[高压缩比的设置比较受欢迎](https://css-tricks.com/brotli-static-compression/)—— （感谢 Jeremy!）
    
    或者，你可以考虑使用 [Zopfli的压缩算法](https://blog.codinghorror.com/zopfli-optimization-literally-free-bandwidth/)，将数据编码为 `Deflate`，`Gzip` 和 `Zlib` 格式。Zopfli 改进的 Deflate 编码使得任何使用 Gzip 压缩的文件受益，因为这些文件大小比 用Zlib 最强压缩后还要小 3％ 到 8％。问题在于压缩文件的时间是原来的大约 80倍。这就是为什么虽然 使用 Zopfli 是一个好主意但是变化并不大，文件都需要设计为只压缩一次可以多次下载的。
    
    比较好的方法是你可以绕过动态压缩静态资源的成本。Brotli 和 Zopfli 都可以用于明文传输 —— HTML，CSS，SVG，JavaScript 等。
    
    有什么方法呢？在最高等级和 Brotli 的 1-4 级动态压缩 HTML [使用Brotli+Gzip 预压缩静态资源](https://css-tricks.com/brotli-static-compression/)。同时，检查 Brotli 是否支持 CDN，（例如KeyCDN，CDN77，Fastly）。确保服务器能够使用 Brotli 或 gzip 处理内容。如果你不能安装或者维护服务器上的 Brotli，那么请使用 Zopfli。

18. **使用 [响应式图像](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/) 和 [WebP](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/)**

    尽可能通过 `srcset`，`sizes` 和 `<picture>` 元素使用[响应式图片](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/)。也可以通过 `<picture>` 元素使用 [WebP格式的图像](https://www.smashingmagazine.com/2015/10/webp-images-and-performance/)（Chrom，Opera，Firefox soon支持），或者一个 JPEG 的回调（见 Andreas Bovens 的 [code snippet](https://dev.opera.com/articles/responsive-images/#different-image-types-use-case)）或者通过使用内容协商（使用 Accept 头信息）。Ire Aderinokun 中也有一个关于 [将图像转换为WebP非常详细的教程](https://bitsofco.de/why-and-how-to-use-webp-images-today/)。
    
    Sketch 本身就支持 WebP，并且 WebP 图像可以通过使用 [WebP插件](http://telegraphics.com.au/sw/product/WebPFormat#webpformat) 从 PhotoShop 中导出。您也有 [其他选择](https://developers.google.com/speed/webp/docs/using) 可以使用。你可以使用 WordPress 或者 Joomla，也有其他可以轻松支持 WebP 的扩展，例如 [Optimus](https://wordpress.org/plugins/optimus/) 和 [Cache Enabler](https://wordpress.org/plugins/cache-enabler/) 以及 [Joomla自己支持的扩展](https://extensions.joomla.org/extension/webp/)（通过 [Cody Arsenault](https://css-tricks.com/comparing-novel-vs-tried-true-image-formats/)）。
    
    您需要注意的是，虽然WebP图像文件大小与 [Guetzli和Zopfli相比大小都差不多](https://www.ctrl.blog/entry/webp-vs-guetzli-zopfli)，但格式 [不支持像 JPEG 这样的渐进式渲染](https://youtu.be/jTXhYj2aCDU?t=630)，这就是为什么用户在使用良好的旧 JPEG 时会更快地看到实际图像，尽管 WebP 图像可能在网络中加载速度会更快。使用 JPEG，我们可以用一半甚至四分之一的数据保证良好的用户体验，然后再加载其余的数据，而不会像WebP那样显示半空的图像。您的决定取决于您的目标：如果您使用WebP，那么将会减少网络的负载，如果使用JPEG，您将提高用户体验。
    
    在 Smashing Magazine 上，我们使用后缀-opt作为图像名称—例如brotli-compression-opt.png;每当图像包含该后缀时，团队中的成员就会知道该图像已经被优化。还有 —— shamleless plug!-Jeremy Wagner 在 [WebP上发表了一本Smashing书](https://www.smashingmagazine.com/ebooks/the-webp-manual/)。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866e7b0a19d994?w=1600&h=915&f=jpeg&s=136508)
    [响应式图像断点生成器](https://www.responsivebreakpoints.com/)自动生成图像和标记生成。

19. **图像是否恰当优化**

    现在有一个至关重要着陆页，有一个特定的图片的加载速度非常关键，确保 JPEGs 是渐进式的并且使用Adept、[mozJPEG](https://github.com/mozilla/mozjpeg)（通过操纵扫描级来改善开始渲染时间）或者 [Guetzli](https://github.com/google/guetzli) 压缩，谷歌新的开源编码器重点是能够感官的性能，并借鉴 Zopfli 和 WebP。[唯一的不足是](https://medium.com/@fox/talk-the-state-of-the-web-3e12f8e413b3)：处理的时间慢（每百万像素 CPU 一分钟）。至于 png，我们可以使用 [Pingo](http://css-ig.net/pingo) 和 svgo，对于 SVG 的处理，我们使用 [SVGO](https://www.npmjs.com/package/svgo) 或 [SVGOMG](https://jakearchibald.github.io/svgomg/)。
    
    每一个图像优化的文章会说明，但始终会提醒要保持矢量资源干净和紧密。确保清理未使用的资源，删除不必要的元数据，并减少图稿中的路径点数量（从而减少SVG代码）。（感谢，Jeremy！）
    
    不过下面还有一些更好的方法：
    
    - 使用 [Squoosh](https://squoosh.app/) 以最佳压缩级别（有损或无损）压缩，调整大小和操作图像。
    - 使用 [响应式图像断点生成器](https://www.responsivebreakpoints.com/) 或 [Cloudinary](https://cloudinary.com/documentation/solution_overview#account_and_api_setup) 或 [Imgix](https://www.imgix.com/) 等服务来自动优化图片。同样，在许多情况下，单独使用 `srcset` 和 `size` 也会有很不错的效果。
    - 可以使用 [映像堆](https://github.com/filamentgroup/imaging-heap) 检查响应式标记的效率，这是一种命令行工具，也可以用来测量视口大小和设备像素比率的效率。
    - 延迟加载带有 [lazysizes](https://github.com/aFarkas/lazysizes) 的图像和iframe，这是一个库，可以检测页面上通过用户交互（或者我们将在稍后探索的IntersectionObserver）而触发的任何改变。
    - 格外注意那些会默认加载但可能永远不会显示的图像——例如carousels、accordions和image galleries。
    - 考虑通过根据媒体查询指定不同的图像显示尺寸来 [交换具有sizes属性](https://www.filamentgroup.com/lab/sizes-swap/) 的图像，例如操纵sizes以交换放大镜组件中的源。
    - 检查图像 [下载的不一致性](https://csswizardry.com/2018/06/image-inconsistencies-how-and-when-browsers-download-images/)，以防止对前景和背景图片的意外下载。
    - 为了优化内部存储，你可以使用 Dropbox 新的 [Lepton格式](https://github.com/dropbox/lepton) 进行压缩，平均将jpeg压缩22%。
    - 注意 [aspect-ratio CSS](https://drafts.csswg.org/css-sizing-4/#ratios) 和 [intrinsicsize-attribute](https://github.com/ojanvafai/intrinsicsize-attribute) 中的属性，它们允许我们为图像设置宽高比和size，因此浏览器可以提前预留一个预定义的布局槽，以 [避免](https://24ways.org/2018/jank-free-image-loads/) 在页面加载期间出现 [布局跳转](https://24ways.org/2018/jank-free-image-loads/)。
    - 如果你想使用其他方式，你可以尝试 [Edge worker](https://youtu.be/jTXhYj2aCDU?t=854) (一种基于CDN的实时过滤器)来剪切和重新排列HTTP/2流，从而更快地通过网络发送图片。Edge workers 使用您可以控制的块的JavaScript流(基本上它们是在CDN边缘上运行的可以修改流式响应的JavaScript)，所以可以控制图像的传递。对于server worker 来说，为时已晚，因为您无法控制在线上的内容，但Edge workers 来说确实有效。因此，您可以在针对特定登录页面逐步保存的静态JPEG之上使用它们。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866edf3e51c32a?w=1600&h=1045&f=jpeg&s=190320)
    [图像堆栈](https://github.com/filamentgroup/imaging-heap) 输出的一个示例，这是一个命令行工具，用于测量视图大小和设备像素比的效率。
    
    随着 [客户端提示(client-hints)](https://cloudfour.com/thinks/responsive-images-201-client-hints/) 的采用，响应图像的未来可能会发生巨大的变化。客户端提示是一个HTTP请求头字段，例如 `DPR`、`Viewport-Width`、`Width`、`Save-Data`、`Accept` (指定图像格式首选项)等。它们通过告知服务器关于用户浏览器、屏幕、连接等的详细信息，然后服务器可以按照详细信息提供如合适格式、合适大小的图片来填充布局。通过客户端提示，我们可以发送一个将资源选择从HTML标记转移到客户端和服务器之间的请求-响应协商。
    
    正如 [Ilya Grigorik所指出的](https://developers.google.com/web/updates/2015/09/automating-resource-selection-with-client-hints)，客户端提示完成了图像——它们不是响应图像的替代方案。`<picture>`元素在HTML标记中提供必要的艺术方向控制。客户端提示为生成的图像请求提供注释，从而支持资源选择自动化。Service Worker在客户端上提供完整的请求和响应管理功能。例如，service Worker可以向请求添加新的客户端提示标头值，以重写URL并将图像请求指向CDN，根据连接和用户首选项等来调整响应。它不仅适用于图像资源，而且还是适用于几乎其他的所有请求。
    
    对于支持客户端提示的客户端，可以在图像上 [节省42%的字节](https://twitter.com/igrigorik/status/1032657105998700544)，在70%以上的百分比上节省1MB以上的字节。在Smashing Magazine上，我们也可以测量 [19-32%的改进](https://www.smashingmagazine.com/2016/01/leaner-responsive-images-client-hints/)。糟糕的是，客户端提示仍然需要 [获得一些浏览器支持](https://caniuse.com/#search=client-hints)，[Firefox正在考虑中](https://bugzilla.mozilla.org/show_bug.cgi?id=935216)。但是，如果同时提供正常响应图像标记和 `<meta>` 客户端提示标记，那么浏览器将评估响应图像标记并使用客户端提示HTTP头请求适当的图像资源。
    
    如果这样子做还不够的话。您还可以使用 [多](https://csswizardry.com/2016/10/improving-perceived-performance-with-multiple-background-images/) [背景](https://jmperezperez.com/medium-image-progressive-loading-placeholder/) [图像](https://manu.ninja/dominant-colors-for-lazy-loading-images#tiny-thumbnails) [技术](https://css-tricks.com/the-blur-up-technique-for-loading-background-images/) 提高图像的性能。请记住，[使用对比度](https://css-tricks.com/contrast-swap-technique-improved-image-performance-css-filters/) 和模糊不必要的细节(或删除颜色)也可以减少文件大小。如果你需要在不影响图片质量的情况下放大一张小照片的话，可以考虑使用 [Letsenhance.io](https://letsenhance.io/)。
    
    到目前为止，这些优化只覆盖了基础。Addy Osmani已经发布了一份非常详细的 [关于基本图像优化的指南](https://images.guide/)，其中深入介绍了图像压缩和颜色管理的细节。例如，您可以模糊掉图像中不必要的部分(通过对它们应用高斯模糊过滤器)以减小文件大小，甚至可以删除颜色或将图像变为黑白，以进一步缩小图像尺寸。如果是背景图像，从Photoshop中导出0到10％质量的照片也是绝对可以接受的。奉劝大家 [不要在网上使用JPEG-XR](https://calendar.perfplanet.com/2018/dont-use-jpeg-xr-on-the-web/)。
    
20. **视频是否已恰当优化**

    到目前为止，我们已经谈论了一些图片，但是我们一直没有说到GIF图片。坦白的说，如果不是加载影响渲染性能和宽带的重型动画GIF，建议最好切换到动画WebP（GIF是后备）或者用 [循环HTML5 video](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/replace-animated-gifs-with-video/) 替换它们。是的，浏览器 [处理 `video` 的速度很慢](https://calendar.perfplanet.com/2017/animated-gif-without-the-gif/#-but-we-already-have-video-tags)，而且与图像不同的是，浏览器不会预加载 `video` 内容，但 `video` 往往要比gif更轻更小。至少我们可以用 [Lossy GIF](https://kornel.ski/lossygif)，[gifsicle](https://github.com/kohler/gifsicle) 或 [giflossy](https://github.com/kornelski/giflossy) 来给GIF添加有损压缩。
    
    早期测试表明，`img` 标签内的内嵌视频 [显示速度提高了20倍](https://calendar.perfplanet.com/2017/animated-gif-without-the-gif/)，解码速度比相同大小的 GIF动图要 [快7倍](https://calendar.perfplanet.com/2017/animated-gif-without-the-gif/)，另外文件大小尺寸也会优于GIF。尽管对 [Safari技术预览版](https://developer.apple.com/safari/technology-preview/release-notes/) 的支持 `<img src=".mp4">` 已经 [落实](https://developer.apple.com/safari/technology-preview/release-notes/)，但还远未被广泛采用，因为它 [不会很快进入Blink](https://bugs.chromium.org/p/chromium/issues/detail?id=791658#c36)。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866f5461954044?w=1600&h=900&f=jpeg&s=139705)
    Addy Osmani [建议](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/replace-animated-gifs-with-video/)用循环的内联视频来替换动画GIF。文件大小的差异很明显(节省了80%)。
    
    然而，在这片充满好消息的土地上，视频格式多年来一直在大规模发展。很长一段时间以来，我们一直希望WebM能够成为规范所有这些格式的格式，而 WebP (基本上是 WebM 视频容器中的一个静态图像)将成为过时的图像格式的替代品。但是，尽管 WebP 和 WebM 最近 [获得了](https://caniuse.com/#feat=webp) [支持](https://caniuse.com/#feat=webm)，可是他们没有什么实质性的突破。
    
    2018年，开放媒体联盟(Alliance of Open Media)发布了一种名为 AV1 的新型视频格式。AV1 的压缩类似于 H.265 编解码器(H.264的演变)，与后者不同的是，AV1是免费的。H.265的收费制使得浏览器厂商开始采用性能 **相对较高** 的 AV1： **AV1(类似H.265)的压缩效果是WebP的两倍**。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866f6b817d2068?w=2560&h=1421&f=png&s=84729)
    AV1很有可能成为网络视频的终极标准。(图片来源:Wikimedia.org)
    
    事实上，苹果目前使用的是HEIF格式和HEVC (H.265)，最新iOS上的所有照片和视频都以这些格式保存，而非JPEG格式。虽然 [HEIF](https://caniuse.com/#search=heif) 和 [HEVC (H.265)](https://caniuse.com/#search=hevc) 还没有完全公开到网络上，但是 AV1 已经完全公开在网络上并且 [正在获得浏览器支持](https://caniuse.com/#feat=av1)。因此，AV1在您的 `<video>`标记中添加源是合理的，因为所有浏览器供应商都在为支持AV1做准备。
    
    目前，最广泛使用和支持的编码是H.264，由MP4文件提供服务，因此在提供文件之前，请确保使用 [多通道编码](https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77) 处理MP4 ，模糊了[frei0r iirblur效果](https://yalantis.com/blog/experiments-with-ffmpeg-filters-and-frei0r-plugin-effects/)（如果适用）和 [moov atom metadata](https://www.adobe.com/devnet/video/articles/mp4_movie_atom.html) 移动到文件的头部，而服务器 [接受字节服务](https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77)。Boris Schapira 为 [FFmpeg](https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77) 提供了最大限度优化视频的 [标准说明](https://medium.com/@borisschapira/optimize-your-mp4-video-for-better-performance-dareboost-blog-fb2f3f3dce77)。当然，提供WebM格式作为替代方案也会有所帮助。
    
    视频播放性能本身就是一个故事，如果您想深入了解它，请阅读Doug Sillar关于 [视频](https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-1/) 和 [视频传输最佳实践的最新实践系列](https://www.smashingmagazine.com/2018/10/video-playback-on-the-web-part-2/)，其中包括关于视频传输度量、视频预加载、压缩和流媒体的详细信息。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/16866f8a3ffc0a36?w=1600&h=974&f=png&s=38483)
    Zach Leatherman的 [字体加载策略综合指南](https://www.zachleat.com/web/comprehensive-webfonts/) 为更好的web字体交付提供了十几种选择。
    
21. **Web 字体已恰当优化**

    首先需要问一个问题，你是否能不使用 [UI 系统字体](https://www.smashingmagazine.com/2015/11/using-system-ui-fonts-practical-guide/)。 如果不可以，那么你有很大可能使用 Web 网络字体，会包含字形和额外的功能以及用不到的加粗。如果您使用的是开源字体，您可以向字体设计公司 [获取](https://www.afasterweb.com/2018/03/09/subsetting-fonts-with-glyphhanger/) 网络字体子集或子集，也可以使用 [Glyphhanger](https://www.afasterweb.com/2018/03/09/subsetting-fonts-with-glyphhanger/) 或 [Fontsquirrel](https://www.fontsquirrel.com/tools/webfont-generator) 对其进行[子集化](https://www.fontsquirrel.com/tools/webfont-generator)。您甚至可以使用 Peter Muller 的 [subfont](https://github.com/Munter/subfont#readme) 将整个流程自动化，因为他是一个命令行工具，它通过静态地分析您的页面，然后生成最优的web字体子集，最后将它们注入到您的页面中。
    
    [WOFF2的支持](https://caniuse.com/#search=woff2) 非常好，对于不支持WOFF2的浏览器，你可以使用 WOFF 和 OTF 作为不支持它的浏览器的备选。另外，从 Zach Leatherman 的 [《字体加载策略综合指南》](https://www.zachleat.com/web/comprehensive-webfonts/)（代码片段也 [可以作为Web字体](https://github.com/zachleat/web-font-loading-recipes) 加载片段）中选择一种策略，并使用服务器缓存持久地缓存字体。
    
    可能今天要考虑的更好的选择是 [关键FOFT预加载](https://www.zachleat.com/web/comprehensive-webfonts/#critical-foft-preload) 和 [**折中** 方法](https://www.zachleat.com/web/the-compromise/)。它们都使用两阶段渲染来逐步提供Web字体——首先是使用web字体快速准确地呈现页面所需的小超子集，然后加载其余的异步操作。不同之处在于，**折中** 技术仅在不支持 [字体加载事件](https://www.igvita.com/2014/01/31/optimizing-web-font-rendering-performance/#font-load-events) 时才异步加载polyfill ，因此默认情况下不需要加载polyfill。需要速战速决吗?Zach Leatherman有一个 [23分钟的快速教程](https://www.zachleat.com/web/23-minutes/) 和案例研究，以使您的字体优化。
    
    通常，使用 `preload` 资源提示来预加载字体是一个好办法，但在标记中要包含关键CSS和JavaScript链接后的提示。否则，字体加载将在第一次渲染时造成损失。不过，有 [选择性](https://youtu.be/FbguhX3n3Uc?t=1637) 地选择最重要的文件可能是一个好主意，比如那些对渲染至关重要的文件，或者那些可以帮助您避免可见和破坏性文本重拍的文件。一般来说，Zach建议 **预加载每个系列的一到两种字体**——如果字体不是很重要，那么建议延迟加载。
    
    我相信没有人喜欢等待内容的显示。使用 [font-display CSS描述符](https://font-display.glitch.me/)，我们可以控制字体加载行为，并使内容立即可读 （`font-display: optional`） 或几乎立即可读 （`font-display: swap`）。但是，如果您想 [避免文本重排](https://www.zachleat.com/web/font-display-reflow/)，我们仍然需要使用字体加载API，特别是对 **重组** 进行 **分组**，或者当您使用第三方主机时，除非您可以 [将Google字体与Cloudflare Workers一起使用](https://blog.cloudflare.com/fast-google-fonts-with-cloudflare-workers/)。谈到谷歌字体:：可以考虑使用 [Google -webfonts-helper](https://google-webfonts-helper.herokuapp.com/fonts)，这是一种轻松自我托管Google字体的方式。如果可以的话，采用 [始终自行托管自身项目的字体](https://speakerdeck.com/addyosmani/web-performance-made-easy?slide=55) 的方式来获得最大程度的控制。
    
    一般情况下，如果您使用font-display: optional，也[可能不是一个好主意](https://www.zachleat.com/web/preload-font-display-optional/)，因为preload会提前触发Web字体请求（如果您有其他需要获取的关键路径资源，则会导致网络拥塞）。使用preconnect可以实现更快的跨域字体的请求，但需要注意的是，preload从不同来源预载的字体wlll会导致网络占用。所有这些技术都包含在 Zach 的 [Web字体加载方式](https://github.com/zachleat/web-font-loading-recipes) 中。
    
    此外，如果用户在可访问性首选项中启用了 [Reduce Motion](https://webkit.org/blog/7551/responsive-design-for-motion/)，或者选择了Data Saver模式(请参见 [Save-Data header](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/save-data/))，或者当用户连接速度较慢时(通过 [网络信息API](https://developer.mozilla.org/en-US/docs/Web/API/Network_Information_API))，则最好选择退出Web字体(或至少是第二阶段渲染)。
    
    要测量Web字体加载性能，请考虑 [所有文本可见](https://noti.st/zachleat/KNaZEg/the-five-whys-of-web-font-loading-performance#s5IYiho) 度量标准（所有字体已加载且所有内容以 Web字体显示的时刻），以及首次渲染后的 [Web字体重排计数](https://noti.st/zachleat/KNaZEg/the-five-whys-of-web-font-loading-performance#sJw0KSc)。显然，两个指标越低，性能越好。重要的是要注意 [可变 字体](https://www.smashingmagazine.com/2017/09/new-font-technologies-improve-web/) 可能需要 [显著的性能考虑](https://youtu.be/FbguhX3n3Uc?t=2161)。它们为设计人员提供了更广阔的设计空间来选择字体，但它的代价是单个串行请求，而不是单个文件请求。单个请求可能会阻碍页面上的整个排版外观。但好消息是，当我们有了可变字体，在默认情况下只需要获得一个 `reflow`，而不需要 `JavaScript` 对重新绘制进行分组。
    
    怎么才能是一个无漏洞的字体加载策略？ 从font-display开始，然后到 Font Loading API，然后到 Bram Stein 的 [Font Face Observer](https://github.com/bramstein/fontfaceobserver)（感谢 Jeremy！）如果你有兴趣从用户的角度来衡量字体加载的性能， Andreas Marschke 探索了 [使用 Font API 和 UserTiming API](https://www.andreas-marschke.name/posts/2017/12/29/Fonts-API-UserTiming-Boomerang.html) 进行 [性能跟踪](https://www.andreas-marschke.name/posts/2017/12/29/Fonts-API-UserTiming-Boomerang.html)。
    
    此外，不要忘记包含 `font-display：optional` 描述符来提供弹性和快速的字体回退，[unicode-range](https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2015/august/how-to-subset-fonts-with-unicode-range/) 将大字体分解成更小的语言特定的字体，以及 Monica Dinculescu 的 [字体样式匹配器](https://meowni.ca/font-style-matcher/) 用来解决由于两种字体之间的大小差异，最大限度地减少了布局上的震动的问题。

### 构建优化

22. **分清轻重缓急**

    你应该知道优先处理什么。运行你所有静态资源（JavaScript、图片、字体、第三方脚本和页面中“昂贵的”模块，比如：轮播图、复杂的图表和多媒体内容），并将它们划分成组。
    
    建立一个电子表格。针对传统浏览器定义基本的核心体验(即完全可访问的核心内容)，针对多功能的浏览器定义增强的体验(即丰富的、完整的体验)和额外的体验(不是绝对需要的并且可以延迟加载的资源，如web字体、不必要的样式、轮播图、视频播放器、社交媒体按钮、大图片等)。不久前，我们发表了一篇关于 [**Improving Smashing Magazine的性能**](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/) 的文章，上面有该方法的详细介绍。
    
    我们在优化性能时候的优先级是：首先加载核心体验，然后是增强功能，最后才是附加功能。

23. **考虑使用 `cutting-the-mustard` 技术**

    现在，我们仍然可以使用 [cut -the-mustard 技术](https://www.filamentgroup.com/lab/modernizing-delivery.html) 将核心体验传递给传统浏览器，并提高对现代浏览器的体验。该技术的 [下一版本](https://snugug.com/musings/modern-cutting-the-mustard/) 将使用 **ES2015 + `<script type="module">`**。现代浏览器会将脚本解释为JavaScript模块并按预期运行，而传统浏览器不会识别该属性并忽略它，因为它是未知的 HTML 语法。
    
    目前我们需要记住的是，仅仅是特征检测不足以做出关于将有效载荷发送到浏览器的决定。从其自身来看，cutting-the-mustard 可以从浏览器版本中推断出设备的能力，这已经不是我们今天能够做到的事情了。
    
    例如：在发展中国家，廉价的安卓手机主要运行 Chrome，虽然它们的内存和 CPU 有限，但仍能满足要求。最终，使用 [Device Memory Client Hints Header](https://github.com/w3c/device-memory)，我们就能够更可靠地识别出低端设备。现在，只有在 Blink 中才支持 header （通常用于 [client hints](https://caniuse.com/#search=client%20hints)）。因为设备存储也有一个在Chrome 中可以调用的 [JavaScript API](https://developers.google.com/web/updates/2017/12/device-memory)，一种选择是基于 API 的特性检测，只在不支持的情况下回退到 **符合标准** 技术（谢谢，Yoav！）。

24. **解析 `JavaScript` 是昂贵的，所以保持小**

    在处理单页应用程序时，我们需要一些时间来初始化应用程序，然后才能呈现页面。您的设置将需要定制的解决方案，但是您可以注意使用模块和技术来加快初始呈现时间。例如，下面是 [如何调试 React 性能](https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad) 和 [消除常见的 React 性能问题](https://logrocket-blog.ghost.io/death-by-a-thousand-cuts-a-checklist-for-eliminating-common-react-performance-issues/)，以及 [如何在 Angular 中提高性能](https://www.youtube.com/watch?v=p9vT0W31ym8)。通常，大多数性能问题来自于启动应用程序的初始解析时间。
    
    [JavaScript 有成本](https://youtu.be/_srJ7eHS3IM?t=9m33s)，但不一定是文件大小影响性能。解析和执行时间的不同很大程度依赖设备的硬件。在一台普通的手机上（Moto G4），仅解析 1MB （未压缩的）的 JavaScript 大概需要 1.3-1.4 秒，会有 15 - 20% 的时间耗费在手机的解析上。在执行编译过程中，只是用在 JavaScript 准备平均需要 4 秒，在手机上页面展示其主要内容所需的时间（First Meaningful Paint）需要 11 秒。解释：在低端移动设备上，[解析和执行时间可以轻松提高 2 至 5 倍](https://medium.com/reloading/javascript-start-up-performance-69200f43b201)。
    
    作为一个开发人员，为了保证高性能，我们需要找到编写和部署更少 JavaScript 的方法，这就是详细检查每个 JavaScript 依赖项的好处所在。
    
    下面这些工具可以帮助您对依赖关系和可行替代方案的影响做出明智的决定:
    - [webpack-bundle-analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)
    - [Source Map Explorer](https://github.com/danvk/source-map-explorer)
    - [Bundle Buddy](https://github.com/samccone/bundle-buddy)
    - [Bundlephobia](https://bundlephobia.com/)
    - [Webpack size-plugin](https://github.com/GoogleChromeLabs/size-plugin)
    - [Import Cost for Visual Code](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)
    
    使用 Ember 在 2017 年引入的 [二进制模板（ binary templates）](https://emberjs.com/blog/2017/10/10/glimmer-progress-report.html#toc_binary-templates) 可以巧妙的避免解析开销过大。使用它们，Ember的建议：使用二进制模板将 JavaScript 解析替换为 JSON 解析，解析速度可能会更快。(谢谢,Leonardo,Yoav !)
    
    [衡量 JavaScript 的解析和编译时间](https://medium.com/reloading/javascript-start-up-performance-69200f43b201#7557)。我们可以使用综合测试工具和浏览器跟踪来跟踪解析时间，浏览器开发商正在讨论在将来 [公开 RUM-based 的处理时间](https://github.com/w3c/resource-timing/issues/133)。或者，你也可以考虑使用 Etsy 的 [DeviceTiming](https://github.com/danielmendel/DeviceTiming)，一个让你可以指导你的 JavaScript 在任何设备或浏览器上测量解析和执行时间的小工具。
    
    最重要的是：虽然脚本大小很重要，但它并不是一切。因为当脚本大小增加时，解析和编译时间 [不一定会随着脚本的变大而相应的增加](https://medium.com/reloading/javascript-start-up-performance-69200f43b201)。

25. **使用 无用代码移除（`Tree-shaking`） ，作用域提升（`Scope hoisting`）和代码分割（`Code-splitting`）来减少有效负载**

    [Tree-shaking](https://developers.google.com/web/fundamentals/performance/optimizing-javascript/tree-shaking/)是一种清理构建过程的方法，通过只加载生产中实际使用的代码并清除在 [Webpack 中](http://www.2ality.com/2015/12/webpack-tree-shaking.html) 未使用的 `import`。使用 Webpack 和 Rollup，当然我们还可以使用 [scope hoisting(作用域提升)](https://medium.com/webpack/brief-introduction-to-scope-hoisting-in-webpack-8435084c171f)，scope hoisting 允许工具检测哪些 `import` 可以被提升或者可以转换成一个内联函数。有了 Webpack ，你现在可以使用 [JSON Tree Shaking](https://react-etc.net/entry/json-tree-shaking-lands-in-webpack-4-0)。
    
    而且，你需要考虑如何 [编写高效的 CSS 选择器](https://csswizardry.com/2011/09/writing-efficient-css-selectors/) 以及如何 [避免编写臃肿和开销浪费的样式](https://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/)。你也可以使用 Webpack 缩短类名和在编译时使用独立作用域来 [动态地重命名 CSS 类](https://medium.freecodecamp.org/reducing-css-bundle-size-70-by-cutting-the-class-names-and-using-scope-isolation-625440de600b)。
    
    [Code-splitting](https://webpack.js.org/guides/code-splitting/) 是 Webpack 的另一个特性，可将你的代码分解为按需加载的 **块**。并不是所有的 JavaScript 都是必须下载、解析和编译的。一旦你在代码中确定了分割点，Webpack 会处理这些依赖关系和输出文件。这样，在应用发送请求的时候，基本上确保初始的下载足够小并且实现按需加载。Alexander Kondrov 对 [使用 Webpack 和 React 进行代码拆分](https://hackernoon.com/lessons-learned-code-splitting-with-webpack-and-react-f012a989113) 做了精彩的介绍。
    
    另外，考虑使用 [preload-webpack-plugin](https://github.com/GoogleChromeLabs/preload-webpack-plugin) 获取代码拆分的路径，然后使用 `<link rel="preload">` 或者 `<link rel="prefetch">` 提示浏览器预加载它们。[Webpack 内联指令](https://webpack.js.org/guides/code-splitting/#prefetching-preloading-modules) 还提供了一些对 `preload` / `prefetch` 的控制。
    
    在哪里定义分离点？通过追踪哪些 CSS/JavaScript 块被使用和哪些没有被使用。Umar Hansa [解释](https://vimeo.com/235431630#t=11m37s) 了你如何使用 Devtools 的 Code Coverage 来实现。
    
    如果你没有使用 Webpack，那么相比于 Browserify 的输出结果，[Rollup](http://rollupjs.org/) 的输出更好一些。我们在此过程中，可以查看  [rollup-plug -closure-compiler](https://github.com/ampproject/rollup-plugin-closure-compiler) 和 [Rollupify](https://github.com/nolanlawson/rollupify)，它们将 `ECMAScript 2015` 模块转换成一个大的 `CommonJS module` —— 因为根据您对 bundler 和 module system 的选择，小模块的 [性能成本会高得惊人](https://nolanlawson.com/2016/08/15/the-cost-of-small-modules/)。
    
26. **能否将 JavaScript 卸载到 Web Worker 中**

    为了减少对时间与交互的影响，可以考虑将繁重的 JavaScript 卸载到 [Web Worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers) 或通过 Service Worker 进行缓存。
    
    随着代码库的代码量不断增长会导致UI性能出现瓶颈，这会直接导致用户体验降低。这是因为 [DOM 操作在主线程上与 JavaScript 一起运行](https://medium.com/google-developer-experts/running-fetch-in-a-web-worker-700dc33ac854)。通过 [web workers](https://flaviocopes.com/web-workers/)，我们可以将这些繁琐的操作转移到不同线程上的后台进程上运行。web workers 的典型用例是通过 [预取数据和渐进式 web 应用程序](https://blog.sessionstack.com/how-javascript-works-the-building-blocks-of-web-workers-5-cases-when-you-should-use-them-a547c0757f6a)，来提前加载和存储一些数据，以便在需要的时候使用。您还可以使用 [Comlink](https://github.com/GoogleChromeLabs/comlink) 来简化主页和 worker 之间的通信。我们正在无限接近目标，但在这个过程中我们还有一些工作要做。
    
    [Workerize](https://github.com/developit/workerize) 允许你将一个模块移动到一个Web Worker 中，自动将导出的函数反映为异步代理。您可以在 Webpack 中使用 [workerize-loader](https://github.com/developit/workerize-loader) 或者 [worker-plugin](https://github.com/GoogleChromeLabs/worker-plugin)。
    
    请注意，Web Worker 不能访问 DOM，因为 DOM 不是一个 **安全线程**，并且执行的代码需要包含在一个单独的文件中。

27. **能否将 JavaScript 卸载到 WebAssembl 中**

    我们还可以将 JavaScript 转换成 [WebAssembly](https://webassembly.org/)（一种二进制指令格式），然后设计成一个便携式目标，用于编译如 `C/ c++ /Rust`  这种高级语言。它的 [浏览器支持也是非常好](https://caniuse.com/#feat=wasm)，而且随着 [JavaSript 和 WASM 之间的函数调用越来越快](https://hacks.mozilla.org/2018/10/calls-between-javascript-and-webassembly-are-finally-fast-%F0%9F%8E%89/)(至少在Firefox中是这样)，它最近已经可以实现了。
    
    在实际场景中，如果一个在一个较小的数组上，[JavaScript 的性能要优于 WebAssembly，反之则是 WebAssembly 的性能优于 JavaScript](https://medium.com/samsung-internet-dev/performance-testing-web-assembly-vs-javascript-e07506fd5875))。对于大多数 web 应用程序而言，JavaScript是更好的选择，而 WebAssembly 更适合用于类似 web 游戏这种计算密集型的 web 应用程序。所以，切换到 WebAssembly 是否会带来显著的性能提升是值得研究去好好研究一番。
    
    如果你想了解更多关于 WebAssembly 的信息:
    - Lin Clark 曾为 WebAssembly 编写了 [一篇详细的系列文章](https://hacks.mozilla.org/2017/02/a-cartoon-intro-to-webassembly/)。Milica Mihajlija 也写了 [一篇文章](https://blog.logrocket.com/webassembly-how-and-why-559b7f96cd71)，介绍如何在浏览器中运行本地代码，为什么要这样做，以及这对JavaScript和web开发的未来意味着什么。
    - Google Codelabs提供了 [对 WebAssembly 的介绍](https://codelabs.developers.google.com/codelabs/web-assembly-intro/index.html)，这是一门60分钟的课程，您将学习如何使用C语言编写本地代码并将其编译到WebAssembly，然后直接从JavaScript调用它。
    - Alex Danilo 在他的 Google I/O 2017 演讲中 [解释了 WebAssembly 以及它的工作原理](https://www.youtube.com/watch?v=6v4E6oksar0)。另外，Benedek Gagyi 分享了 [一个关于 WebAssembly 的实际案例研究](https://www.youtube.com/watch?v=l2DHjRmgAF8)，具体的告诉我们，团队如何将 WebAssembly 作为 `C++ codebase` 的输出格式，然后在 `ios`，`Android` 和网站上使用。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/1686a639af5b33f0?w=1600&h=792&f=png&s=39746)
    Milica Mihajlija 为我们提供了 [一个关于WebAssembly的工作原理以及它的用处的概述](https://blog.logrocket.com/webassembly-how-and-why-559b7f96cd71)。

28. **您使用的是预编译器吗**

    使用 [预编译器](https://www.lucidchart.com/techblog/2016/09/26/improving-angular-2-load-times/) 可以[将一些客户端渲染卸载到](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/) [服务器](https://redux.js.org/recipes/server-rendering)，从而快速输出可用的结果。最后，可以考虑使用 [optimization.js(https://github.com/nolanlawson/optimize-js) 来封装急切调用的函数(不过 [可能不再需要它了](https://twitter.com/tverwaes/status/809788255243739136))来加快初始加载速度。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/1686a645339fab37?w=1600&h=895&f=jpeg&s=68441)
    Addy Osmani 的 [从快速默认到现代加载的最佳实践](https://speakerdeck.com/addyosmani/fast-by-default-modern-loading-best-practices)。

29. **仅将遗留代码提供给传统浏览器**
    
    随着 [现代浏览器 对 ES2015 的支持](http://kangax.github.io/compat-table/es6/)越来越好，考虑 [使用 babel-preset-env](http://2ality.com/2017/02/babel-preset-env.html) 只转换现代浏览器不支持的 `ES2015+` 的特性。然后 [设置两个构建](https://gist.github.com/newyankeecodeshop/79f3e1348a09583faf62ed55b58d09d9)，一个为 ES6 一个为 ES5。就像上面所说的那样，现在所有 [主流浏览器](https://caniuse.com/#feat=es6-module)都支持 JavaScript 模块，我们可以 [使用 `script type="module"`](https://developers.google.com/web/fundamentals/primers/modules) 让具有 ES 模块支持的浏览器加载文件，而老的浏览器可以加载传统的 `script nomodule`。我们可以使用 [Webpack ESNext Boilerplate](https://github.com/philipwalton/webpack-esnext-boilerplate) 自动完成整个流程。

    请注意，现在我们可以在不需要编译器或绑定器的情况下编写在浏览器中本地运行的基于模块的 JavaScript。[`<link rel="modulepreload">` header](https://developers.google.com/web/updates/2017/12/modulepreload) 提供一种方法来启动模块脚本的早期(高优先级)加载。基本上，这是一种有助于最大化带宽使用的有效方式，通过告知浏览器它需要获取什么，以使其不会在那些长时间往返的过程中被卡住。Jake Archibald 也发表了一篇详细的文章，其中 [介绍了 ES 模块中需要记住的问题和内容](https://jakearchibald.com/2017/es-modules-in-browsers/)，值得一看。
    
    对于 loadsh，[使用 babel-plugin-lodash](https://github.com/lodash/babel-plugin-lodash) 将只加载你仅在源码中使用的模块。您的依赖项可能还依赖于 Lodash 的其他版本，因此您需要 [将通用 lodash 转换成适合自己项目的 loadsh](https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/)，以避免代码重复。这可能会为您节省相当多的 JavaScript 负载。
    
    Shubham Kanodia 编写了一份 [关于智能捆绑的详细低维护指南](https://www.smashingmagazine.com/2018/10/smart-bundling-legacy-code-browsers/)：将遗留代码与您可以立即使用的代码片段一起交付到生产环境中的传统浏览器。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/1686a65b328471bc?w=1600&h=978&f=png&s=47433)
    Jake Archibald 发布了一篇详细的文章，介绍了 [ES 模块中需要记住的问题和内容](https://jakearchibald.com/2017/es-modules-in-browsers/)，例如，内联脚本被推迟到阻塞外部脚本和内联脚本执行时才执行。

30. **您是否在JavaScript中使用差异化服务**

    我们想通过网络发送必要的 JavaScript 代码，但这意味着对这些资源的交付要更加专注和细致。不久前，Philip Walton 提出了[差异化服务](https://philipwalton.com/articles/deploying-es2015-code-in-production-today/) 的概念。其思想是编译并提供两个独立的 JavaScript 包:一个是 **常规** （带有 Babel-transforms 和 polyfill ）的构建包，另一个是没有 Babel-transforms 或 polyfill 的包，这两个包都是只提供给实际需要它们的传统浏览器。
    
    因此，我们通过降低浏览器需要处理的脚本的数量来减少阻塞主线程的进程。Jeremy Wagner 发表了一篇文章，[全面的介绍了差异化服务](https://calendar.perfplanet.com/2018/doing-differential-serving-in-2019/) 以及如何在2019年的构建管道中设置它，从设置 Babel，到需要在 Webpack 中进行哪些调整，以及做这些工作的好处。

31. **通过增量解耦识别和重写遗留代码**

    长期存在的项目有收集灰尘和过时代码的趋势。重新考虑你的依赖，评估需要多少时间来重构或重写那些最近一直在导致问题的遗留代码。如果您了解了遗留代码的影响，您就可以从 [增量解耦](https://githubengineering.com/removing-jquery-from-github-frontend/) 开始解决这项艰巨的任务。
    
    首先，建立一个度量标准，跟踪遗留代码调用的比例，看看是保持不变还是下降，如果调用不是上升，那就公开阻止团队使用这个库，并确保 CI 在 pull 请求中使用得时候可以 [通知](https://github.com/dgraham/eslint-plugin-jquery) 到开发人员。[polyfills](https://githubengineering.com/removing-jquery-from-github-frontend/#polyfills) 可以使用标准浏览器功能帮助遗留代码重写代码库。

32. **识别并删除未使用的 `CSS` / `JavaScript`**

    Chrome 中的 [CSS 和 JavaScript 代码覆盖](https://developers.google.com/web/updates/2017/04/devtools-release-notes#coverage) 允许您了解哪些代码已经执行/应用，哪些代码还没有执行。您可以开始记录覆盖率，在页面上执行操作，然后研究代码覆盖率结果。检测到未使用的代码后，[使用 `import()` 查找这些模块和延迟加载](https://twitter.com/TheLarkInn/status/1012429019063578624)(参见整个线程)。然后重复覆盖率配置文件，并验证它现在在初始加载时提供的代码更少。
    
    您可以使用 [Puppeteer](https://github.com/GoogleChrome/puppeteer) [以编程方式收集代码覆盖率](https://twitter.com/matijagrcic/statuses/1060863620568043520)，Canary 已经允许您 [导出代码覆盖率结果](https://twitter.com/tkadlec/status/1073330247758684163)。正如 Andy Davies 所指出的，您可能希望 [为现代浏览器和传统浏览器收集代码覆盖率](https://twitter.com/AndyDavies/status/1073339071106297856)。对于 [Puppeteer](https://github.com/GoogleChromeLabs/puppeteer-examples)，还有许多 [其他的用例](https://github.com/GoogleChromeLabs/puppeteer-examples)，例如，在每次构建时自动地对未使用的CSS进行[视觉区分](https://meowni.ca/posts/2017-puppeteer-tests/) 或 [监视](http://blog.cowchimp.com/monitoring-unused-css-by-unleashing-the-devtools-protocol/)。
    
    此外，[purgecss](https://github.com/FullHuman/purgecss)、[UnCSS](https://github.com/uncss/uncss) 和 [Helium](https://github.com/geuis/helium-css) 可以帮助您从 CSS 中删除未使用的样式。如果你不确定代码是否被使用，您可以按照 [Harry Roberts的建议](https://csswizardry.com/2018/01/finding-dead-css/)：为一个特定类创建一个 1×1 px 透明的 GIF 图片并将其放在 `dead/` 目录下，例如：`/assets/img/dead/comments.gif`。然后，在CSS中相应的选择器上将特定的图像设置为背景，如果文件出现在日志中，则等待几个月。如果文件没有出现在日志中，那就是没有人在屏幕上渲染该遗留组件，您可以把它全部删除。
    
    对于一个有想法的小伙伴来说，可以考虑通过 [使用并监视DevTools](http://blog.cowchimp.com/monitoring-unused-css-by-unleashing-the-devtools-protocol/)，在一组页面上自动收集未使用的 CSS。

33.  **修剪 `JavaScript` 依赖项的大小**

    正如 [Addy Osmani 所指出的](https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4)，当您只需要一小部分 JavaScript库时，您很可能会提供完整的JavaScript 库，以及不需要这些库的浏览器的过时 polyfill，或者只是重复代码。为了避免这种开销，可以考虑使用 [webpack-libs-optimization](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)来删除构建过程中未使用的方法和 [polyfill](https://github.com/GoogleChromeLabs/webpack-libs-optimizations)。
    
    将捆绑审核对于您多年前添加的大型库，可能有一些轻量级的替代方案，例如Moment.js可以用 [date-fns](https://github.com/date-fns/date-fns) 或 [Luxon](https://moment.github.io/luxon/) 代替。[BenediktRötsch 的研究](https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/) 表明，从 `Moment.js` 到 `date-fns` 的转换可能会使 3G 和低端手机上的首次使用时间节省大约 300ms。
    
    这就是像 [Bundlephobia](https://bundlephobia.com/) 这样的工具可以帮助我们监测到向包中添加 npm 包的成本。您甚至可以 [将这些成本与 Lighthouse Custom Audit 相结合](https://github.com/AymenLoukil/Google-lighthouse-custom-audit)。这也适用于框架。通过删除或修剪 [Vue MDC适配器](https://speakerdeck.com/addyosmani/web-performance-made-easy?slide=22)([Vue的材料组件](https://speakerdeck.com/addyosmani/web-performance-made-easy?slide=22))，样式大小从 194KB 下降到 10KB。
    
    喜欢冒险吗？你可以看看 [Prepack](https://gist.github.com/gaearon/d85dccba72b809f56a9553972e5c33c4)。它将JavaScript 编译成等效的 JavaScript 代码，但与 Babel 或 Uglify 不同的是，它允许编写正常的 JavaScript 代码，并输出运行速度更快的等效 JavaScript 代码。
    
    作为整个框架的替代，您甚至可以修剪框架并将其编译为不需要额外代码的原始JavaScript包。[Svelte 做到了](https://svelte.technology/)，还有 [Rawact Babel plugin 也做到了](https://github.com/sokra/rawact)。在构建时将 `React.js ` 组件转换为本地 DOM 操作。为什么？正如维护者所解释的，**react-dom** 包含了所有可能被渲染的组件/`HTMLElement` 的代码，包括用于增量渲染、调度、事件处理等的代码。但是有些应用程序(在初始页面加载时)不需要所有这些特性。对于这样的应用程序，使用原生DOM操作来构建交互式用户界面可能更好。
    
    ![](https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_auto/w_1600/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e30c7d5b-ef8b-46ba-b0fc-b1d5a31cefff/webpack-comparison.png)
    在 [Benedikt Rotsch 的文章](https://www.contentful.com/blog/2017/10/27/put-your-webpack-bundle-on-a-diet-part-3/) 中，展示了一个从 `Moment.js` 到 `date-fns`，在 3G 和低端手机上首次使用时，可以节省大约 300ms 的时间的转变。

34. **您是否正在使用 `JavaScript` 块的预测预取**

    我们可以使用 heuristics 来决定何时预加载 JavaScript 块。[Guess.js](https://github.com/guess-js/guess) 是一套使用谷歌分析数据的工具和库，用来确定用户最可能从特定页面访问的页面。根据从谷歌分析或其他来源收集的用户导航模式，[Guess.js](https://github.com/guess-js/guess) 构建了一个机器学习模型来预测和预取每个后续页面所需的 JavaScript。
    
    因此，每个交互元素都会收到一个参与概率得分，基于这个分数，客户端脚本决定提前预取资源。你可以把这项技术应用到 [Next.js application](https://github.com/mgechev/guess-next)，[Angular和React](https://blog.mgechev.com/2018/03/18/machine-learning-data-driven-bundling-webpack-javascript-markov-chain-angular-react/)，还有一个 [Webpack 插件](https://github.com/guess-js/guess/tree/master/packages/guess-webpack)，它也可以自动完成设置过程。
    
    显然，很明显，你可能会让浏览器读取不需要的数据并提前获取不需要的页面，所以在这些预先获取的请求的数量上做个相对保守的选择是个好主意。一个好的用例在检查过程中预取所需的验证脚本，或者在关键的动作调用进入视图时进行预取。
    
    需要不那么复杂的东西吗？[Quicklink](https://github.com/GoogleChromeLabs/quicklink) 是一个小库，它在空闲时间自动预取视图中的链接，以加快加载下一页导航的速度。不过，它也考虑到了数据，因此它不会在 2G 或 `Data-Saver` 时预取。

35. **利用针对目标JavaScript引擎的优化**    

    研究 JavaScript 引擎在用户基础中占的比例，然后探索优化它们的方法。例如，当优化的 V8 引擎是用在 Blink 浏览器，`Node.js` 运行和 Electron 的时候，对每个脚本使用脚本流。一旦下载开始，它允许 `async` 或 `defer scripts`在一个单独的后台线程进行解析，因此在某些情况下，提高 10% 的页面加载时间。实际上，在 `<head>` 中使用 `<script defer>`，以便 [浏览器更早地可以发现资源](https://medium.com/reloading/javascript-start-up-performance-69200f43b201#3498)，然后在后台线程中解析它。
    
    警告：Opera Mini [不支持 `defement` 脚本](https://caniuse.com/#search=defer)，如果你正在印度和非洲从事开发工作，`defer` 将会被忽略，导致阻塞渲染直到脚本加载（感谢 Jeremy）!。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/1686a6ad9d818dd8?w=1600&h=763&f=jpeg&s=86075)
    [渐进引导](https://aerotwist.com/blog/when-everything-is-important-nothing-is/)：使用服务器端渲染获得首次有效绘制，但也包含一些最小必要的 JavaScript 来保持实时交互来接近首次有效绘制。

36. **客户端渲染还是服务器端渲染**

    在两种场景下，我们的目标应该是建立 [渐进引导](https://aerotwist.com/blog/when-everything-is-important-nothing-is/)：使用服务端呈现获得首次有效绘制，而且还要包含一些最小必要的 JavaScript 来保持实时交互来接近首次有效绘制。如果 JavaScript 在首次有效绘制没有获取到，那么浏览器可能会在解析时 [锁住主线程](https://davidea.st/articles/measuring-server-side-rendering-performance-is-tricky)，编译和执行最新发现的 JavaScript，从而对 [站点或应用程序](https://philipwalton.com/articles/why-web-developers-need-to-care-about-interactivity/) 的 [交互性](https://philipwalton.com/articles/why-web-developers-need-to-care-about-interactivity/) 造成限制。
    
    为了避免这样做，总是将执行函数分离成一个个，异步任务和可能用到 `requestIdleCallback` 的地方。考虑 UI 的懒加载部分使用 WebPack 动态 [import()支持](https://developers.google.com/web/updates/2017/11/dynamic-import)，避免加载、解析和编译开销直到用户真的需要他们（感谢 Addy!）。
    
    在本质上，交互时间（TTI）告诉我们导航和交互之间的时间。度量是通过在窗口初始内容呈现后的第一个五秒来定义的，在这个过程中，JavaScript 任务都不超过 50ms。如果发生超过 50ms 的任务，则重新开始搜索五秒钟的窗口。因此，浏览器首先会假定它达到了交互式(Interactive)，只是切换到冻结状态(Frozen)，最终切换回交互式(Interactive)。
    
    一旦我们达到交互式(Interactive)，然后，我们可以按需或等到时间允许，启动应用程序的非必需部分。不幸的是，随着 [Paul Lewis 提到的](https://aerotwist.com/blog/when-everything-is-important-nothing-is/#which-to-use-progressive-booting)，框架通常没有优先级的概念，因此渐进式引导很难用大多数库和框架实现。如果你有时间和资源，使用该策略可以极大地改善前端性能。
    
    是在客户端渲染还是服务器端渲染？如果对用户的体验没有明显的提升，那么 [可能我们不会在客户端渲染](https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4)，因为在实际情况中，服务器端渲染的HTML可能更快。或许，您可以 [用静态站点生成器预先加载一些内容](https://jamstack.org/) 直接推到 CDN 上，并在顶部使用一些 JavaScript。
    
    将客户端框架的使用限制在绝对需要它们的页面上。为了防止服务器渲染比客户端渲染慢，可以考虑 [在构建时预渲染](https://github.com/GoogleChromeLabs/prerender-loader) 和动态 [CSS 内联](https://github.com/GoogleChromeLabs/critters)，以生成可用于生产的静态文件。Addy Osmani 做了一个关于 [JavaScript 成本](https://www.youtube.com/watch?v=63I-mEuSvGA) 的 [精彩演讲](https://www.youtube.com/watch?v=63I-mEuSvGA)，值得一看。

37. **限制第三方脚本的影响**

    随着所有性能优化的到位，我们常常无法控制来自业务需求的第三方脚本。第三方脚本的度量不受用户体验的影响，所以，一个单一的脚本常常会以调用令人讨厌的，长长的第三方脚本为结尾，因此，破坏了为性能专门作出的努力。为了控制和减轻这些脚本带来的性能损失，仅异步加载（[可能通过 `defer`](https://www.twnsnd.com/posts/performant_third_party_scripts.html)）和通过资源提示，如：`dns-prefetch` 或者 `preconnect` 加速他们是不足够的。
    
    正如 Yoav Weiss 在他的 [必须关注第三方脚本的通信](http://conffab.com/video/taking-back-control-over-third-party-content/) 中解释的，在很多情况下，下载资源的这些脚本是动态的。页面负载之间的资源是变化的，因此我们不知道主机是从哪下载的资源以及这些资源是什么。
    
    这时，我们有什么选择？考虑**通过一个超时来使用 service workers 下载资源**，如果在特定的时间间隔内资源没有响应，返回一个空的响应告知浏览器执行解析页面。你可以记录或者限制那些失败的第三方请求和没有执行特定标准请求。您还可以选择，从 [您自己的服务器](https://medium.com/caspertechteam/we-shaved-1-7-seconds-off-casper-com-by-self-hosting-optimizely-2704bcbff8ec) 而不是从供应商的服务器 [加载第三方脚本](https://medium.com/caspertechteam/we-shaved-1-7-seconds-off-casper-com-by-self-hosting-optimizely-2704bcbff8ec)。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/1686a6dbfe441242?w=1600&h=801&f=png&s=26935)
    Casper.com 发表了[一篇详细的案例研究](https://medium.com/caspertechteam/we-shaved-1-7-seconds-off-casper-com-by-self-hosting-optimizely-2704bcbff8ec)，讲述了他们是如何通过自我托管的优化，使网站缩短了 1.7s。这也许是值得的。
    
    另一个选择是建立一个 **内容安全策略（CSP）** 来限制第三方脚本的影响，比如：不允许下载音频和视频。最好的选择是通过 `<iframe>` 嵌入脚本使得脚本运行在 `iframe` 环境中，因此如果没有接入页面 DOM 的权限，在你的域下不能运行任何代码。`Iframe` 可以 使用 `sandbox` 属性进一步限制，因此你可以禁止 `iframe` 的任何功能，比如阻止脚本运行，阻止警告、表单提交、插件、访问顶部导航等等。
    
    例如，它可能必须要允许脚本运行 `<iframe sandbox="allow-scripts">`。每一个限制都可以通过多种 `[allow` 在 `sandbox` 属性中（[几乎处处支持](https://caniuse.com/#search=sandbox)）解除，所以将它们限制在允许做的最低限度。
    
    考虑使用Intersection Observer；这将使广告嵌入 `iframe` 的同时仍然调度事件或需要从 DOM 获取信息（例如广告知名度）。注意新的策略如 [功能策略](https://www.smashingmagazine.com/2018/12/feature-policy/)、资源的大小限制、CPU 和带宽优先级限制损害的网络功能和会减慢浏览器的脚本，例如：同步脚本，同步 XHR 请求，`document.write` 和超时的实现。
    
    要 [对第三方进行压力测试](https://csswizardry.com/2017/07/performance-and-resilience-stress-testing-third-parties/)，在 DevTools 上自底向上概要地检查页面的性能，测试在请求被阻止或超时后会发生什么情况，对于后者，你可以使用 WebPageTest 的 Blackhole 服务器 `Blackhole .webpagetest.org`，你可以在你的 hosts 文件中指定特定的域名。最好是 [自主主机并使用单个主机名](https://www.twnsnd.com/posts/performant_third_party_scripts.html)，但是同时 [生成一个请求映射](https://www.soasta.com/blog/10-pro-tips-for-managing-the-performance-of-your-third-party-scripts/)，当脚本变化时，暴露给第四方调用和检测。您可以使用 Harry Roberts 的方法来 [审计第三方](https://csswizardry.com/2018/05/identifying-auditing-discussing-third-parties/)，并生成 [这样的](https://docs.google.com/spreadsheets/d/1uTcRSoJAkXfIm2yfG5hvCSzvSZD9fAwXNQMVK3HdPMI/edit#gid=0) 电子表格。Harry 还在他 [关于第三方性能和审计的演讲](https://www.youtube.com/watch?v=bmIUYBNKja4) 中解释了审计工作流。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/1686a6f96d364e97?w=1600&h=954&f=jpeg&s=100359)
    图片来源： [Harry Roberts](https://csswizardry.com/2017/07/performance-and-resilience-stress-testing-third-parties/#request-blocking)

38. **正确设置 HTTP 缓存头**

    再次检查一遍 `expires`，`cache-control`，`max-age` 和其他 HTTP cache 头部都是否设置正确。通常，资源应该是可缓存的，[不管是短时间的（如果它们很可能改变），还是无限期的（如果它们是静态的）](https://jakearchibald.com/2016/caching-best-practices/)——你可以在需要更新的时候，改变它们 URL 中的版本即可。在任何资源上禁止头部 `Last-Modified` 都会导致一个 `If-Modified-Since` 条件查询，即使资源在缓存中。与 Etag 一样，即使它在使用中。
    
    使用 `Cache-control: immutable`，其实是为了解决fingerprinted静态资源的缓存问题而被设计出来的，解决了客户端revalidation问题（截至 2017年12月，[在 FireFox，Edge 和 Safari 中支持](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)；只有 FireFox 在 `https://` 中支持）。实际上，HTTP存档中的所有页面，2% 的请求和 30% 的站点几乎都包含 [至少1个不可更改的响应](https://discuss.httparchive.org/t/cache-control-immutable-a-year-later/1195)。此外，大多数使用它的网站都有一个指令，这个指令是对资源具有较长的新鲜度生命周期。
    
    还记得 [stale-while-revalidate](https://www.fastly.com/blog/stale-while-revalidate-stale-if-error-available-today) 吗？您可能知道，我们使用 `Cache-Control` 响应头指定缓存时间，例如：`Cache-Control: max-age=604800`。等到 604800s 过后，缓存会重新获取请求的内容，这直接导致页面加载速度变慢。我们可以使用 `stale-while-revalidate` 来避免这种情况的发生：它基本上是定义了一个额外的时间窗口，只要在此期间后台重新验证它的异步性，那么缓存久可以直接使用过期的资源。因此，它在客户端可以 **隐藏** 延迟(包括网络和服务器上的延迟)。
    
    在2018年10月，Chrome 发布了一个 [意图](https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/rspPrQHfFkI/discussion)，打算在 `HTTP Cache-Control` 报头中提供 `stale-while-revalidate`，因此，随着过期资源不再处于关键的状态，它将会提高后续页面的加载时间。结果：[重复视图的RTT为零](https://twitter.com/RyanTownsend/status/1072443651844911104)。
    
    你也可以使用 [Heroku 的 HTTP 缓存头部](https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers)，Jake Archibald 的 [ 缓存最佳实践(Caching Best Practices)](https://jakearchibald.com/2016/caching-best-practices/) ，以及 Ilya Grigorik 的 [HTTP缓存入门(HTTP caching primer)](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=en) 作为指导。而且，注意 [不同的头部](https://www.smashingmagazine.com/2017/11/understanding-vary-header/)，尤其是在 [关系到 CDN 时](https://www.fastly.com/blog/getting-most-out-vary-fastly)，并且要注意 [关键头文件](https://www.greenbytes.de/tech/webdav/draft-ietf-httpbis-key-latest.html)，有助于避免在新请求稍有差异时进行额外的验证，但从以前请求标准，并不是必要的（感谢，Guy！）。
    
    另外，要仔细检查您是否发送了 [不必要的标题](https://www.fastly.com/blog/headers-we-dont-want) (例如，`x-power -by`、`pragma`、`x-ua-compatible`、`expires`等)，以及是否包含了 [有用的安全性和性能标题](https://www.fastly.com/blog/headers-we-want) (例如 `Content-Security-Policy`、`X-XSS-Protection`、`X-Content-Type-Options`等)。最后，请记住单页面应用程序中 [CORS请求的性能成本](https://medium.com/@ankur_anand/the-terrible-performance-cost-of-cors-api-on-the-single-page-application-spa-6fcf71e50147)。

### 交付优化

39. **异步加载JavaScript**

    当用户请求页面时，浏览器获取 HTML 并构造 DOM，然后获取 CSS 并构造 CSSOM，然后通过匹配 DOM 和 CSSOM 生成一个渲染树。如果有任何的 JavaScript 需要解决，浏览器将不会开始渲染页面，直到 JavaScript 解决完毕，这样就会延迟渲染。 作为开发人员，我们必须明确告诉浏览器不要等待并立即开始渲染页面。 为脚本执行此操作的方法是使用 HTML 中的 `defer` 和 `async` 属性。
    
    事实证明，我们 [应该 把 `async` 改为 `defer`](https://calendar.perfplanet.com/2016/prefer-defer-over-async/)（因为 [ie9 及以下](https://github.com/h5bp/lazyweb-requests/issues/42) 不支持 `async`）。根据 [Steve Souders](https://youtu.be/RwSlubTBnew?t=1034) 的说法，一旦加载到 `async` 脚本时，它们就会立即执行。如果这种情况发生得非常快，并且 `async` 脚本已经处于缓存中时，它实际上会阻塞 HTML 解析器。所以我们可以使用延迟，来保证浏览器在解析 HTML 之前不会执行脚本。因此，除非您在开始渲染之前需要执行 JavaScript ，否则最好使用 `defer`。
    
    另外，从上面的描述来看，我们需要限制第三方库和脚本的影响，特别是使用社交共享按钮和嵌入的 `<iframe>`（如地图）。[大小限制](https://github.com/ai/size-limit) 有助于 [防止 JavaScript 库过大](https://evilmartians.com/chronicles/size-limit-make-the-web-lighter)：如果您不小心添加了大量依赖项，该工具将通知您并抛出错误。您可以使用静态社交分享按钮（如通过 [SSBG](https://simplesharingbuttons.com/)）和 [静态链接来代替交互式地图](https://developers.google.com/maps/documentation/static-maps/intro)。您还可以 [修改非阻塞脚本加载程序以实现 CSP 合规性](https://calendar.perfplanet.com/2018/a-csp-compliant-non-blocking-script-loader/)。

40. **使用 [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) 延迟加载昂贵的组件**

    如果您需要延迟加载图片、视频、广告脚本、A/B 测试脚本或任何其他资源，最有效的方法是使用 [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)，该 API 提供了一种 异步观察目标元素与祖先元素或顶级文档视口的交集变化的方法。基本上，您需要创建一个新的 `IntersectionObserver` 对象，它接收回调函数和一组选项。然后我们添加一个目标来观察。
    
    当目标变得可见或不可见时，回调函数就会执行，因此当它拦截viewport时，您可以在元素变得可见之前开始执行一些操作。事实上，我们可以精确地控制观察者的回调何时被调用，使用 `rootMargin` 和 `threshold`（一个数字或者一个数字数组来表示目标可见度的百分比）。
    
    Alejandro Garcia Anglada 发表了一个关于如何在实际应用场景当中去实现它的 [简易教程](https://medium.com/@aganglada/intersection-observer-in-action-efc118062366)，Rahul Nanwani 写了一篇详细介绍 [关于延迟加载前景和背景图像](https://css-tricks.com/the-complete-guide-to-lazy-loading-images/) 的 [文章](https://developers.google.com/web/fundamentals/performance/lazy-loading-guidance/images-and-video/)，Google Fundamentals 也提供了一篇 [关于 Intersection Observer 延迟加载图像和视频](https://developers.google.com/web/fundamentals/performance/lazy-loading-guidance/images-and-video/) 的 [详细教程](https://developers.google.com/web/fundamentals/performance/lazy-loading-guidance/images-and-video/)。您也可以 [使用 Intersection Observer](https://github.com/russellgoldenberg/scrollama) 实现 [高效的滚动测试(performant scrollytelling)](https://github.com/russellgoldenberg/scrollama)。
    
    另外，请关照一下 [lazyload](https://css-tricks.com/a-native-lazy-load-for-the-web-platform/)，它是一个允许我们指定哪些图像和 `iframes` 应该本地延迟加载的 `attribute`。功能策略：LazyLoad 将提供一种允许我们在每个域的基础上强制选择是否使用 LazyLoad 功能的机制(类似于 [内容安全策略](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) 的工作方式)。额外的好处:一旦发布，[优先级提示](https://twitter.com/csswizardry/status/1050717710525509633)将允许我们在标题中指定脚本和预加载的重要性(目前在 Chrome Canary 中)。
    
41. **逐步加载图像**

    你甚至可以通过向你的网页添加 [渐进式图片加载](https://www.guypo.com/introducing-lqip-low-quality-image-placeholders) 来将延迟加载提升到新的水平。 与 Facebook，Pinterest 和 Medium 类似，你可以先加载低质量或模糊的图像，然后当页面继续加载时，使用 Guy Podjarny 提出的 [LQIP (Low Quality Image Placeholders) technique（低质量图像占位符）技术](https://www.guypo.com/introducing-lqip-low-quality-image-placeholders) 替换它们的清晰版本。
    
    如果技术改善了用户体验，观点就不一样了，但它肯定会提高第一次有意义的绘画的时间。我们甚至可以通过使用 [SQIP](https://github.com/technopagan/sqip) 创建图像的低质量版本作为 SVG 占位符或者使用带有 CSS 线性渐变的 [渐变图像占位符](https://calendar.perfplanet.com/2018/gradient-image-placeholders/) 来实现自动化。 这些占位符可以嵌入 HTML 中，因为它们自然可以用文本压缩方法压缩。 Dean Hume 在 [他的文章](https://calendar.perfplanet.com/2017/progressive-image-loading-using-intersection-observer-and-sqip/) 中描述了如何使用 Intersection Observer 来实现这种技术。
    
    浏览器支持吗？[可以说相当好](https://caniuse.com/#feat=intersectionobserver)，Chrome、Firefox、Edge 和 Samsung Internet 这些浏览器都已经支持。WebKit 目前 [正在开发中](https://webkit.org/status/#specification-intersection-observer)。如果浏览器不支持呢？ 如果不支持Intersection Observer，我们仍然可以 [延迟加载](https://medium.com/@aganglada/intersection-observer-in-action-efc118062366) 一个 [polyfill](https://github.com/jeremenichelli/intersection-observer-polyfill) 或立即加载图像。甚至还有一个 [库(library)](https://github.com/ApoorvSaxena/lozad.js)。
    
    想把延迟加载做到极致？您可以尝试着 [跟踪图像](https://jmperezperez.com/svg-placeholders/)，并使用原始形状和边缘创建轻量级SVG占位符，先加载它，然后从占位符矢量图像过渡到(加载的)位图图像。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/1686a5883061998e?w=1600&h=803&f=jpeg&s=68562)
    Jose M. Perez的 [SVG 延迟加载技术](https://jmperezperez.com/svg-placeholders/)。

42. **快速推送关键 CSS**

    为确保浏览器尽快开始渲染页面，[通常](https://www.smashingmagazine.com/2015/08/understanding-critical-css/) 会收集开始渲染页面的第一个可见部分所需的所有 CSS（称为 **关键CSS** 或 **首屏 CSS**）并将其内联添加到页面的 `<head>` 中，从而减少往返。 由于在慢启动阶段交换包的大小有限，所以关键 CSS 的预算大约是 14 KB。
    
    如果超出这个范围，浏览器将需要额外往返取得更多样式。[CriticalCSS](https://github.com/filamentgroup/criticalCSS) 和 [Critical](https://github.com/addyosmani/critical) 可以做到这一点。 你可能需要为你使用的每个模板执行此操作。 如果可能的话，考虑使用 Filament Group 使用的 [条件内联方法](https://www.filamentgroup.com/lab/modernizing-delivery.html)，或者 [动态地将内联代码转换为静态资产](https://www.smashingmagazine.com/2018/11/pitfalls-automatically-inlined-code/)。
    
    使用 HTTP/2，关键 CSS 可以存储在一个单独的 CSS 文件中，并通过 [服务器推送](https://www.filamentgroup.com/lab/modernizing-delivery.html) 来传递，而不会增大 HTML 的大小。 问题在于，服务器推送是很 [麻烦](https://twitter.com/jaffathecake/status/867699157150117888)，因为浏览器中存在许多问题和竞争条件。 它一直不被支持，并有一些缓存问题（参见 [Hooman Beheshti介绍的文章](Hooman Beheshti's presentation) 114 页内容）。事实上，这种影响可能是 [负面的](https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/)，会使网络缓冲区膨胀，从而阻止文档中的真实帧被传送。 而且，由于 TCP 启动缓慢，似乎服务器推送 [在热连接上更加有效](https://docs.google.com/document/d/1K0NykTXBbbbTlv60t5MyJvXjqKGsCVNYHyLEXIxYMv0/edit)。
    
    即使使用 HTTP/1，将关键 CSS 放在根目录上的单独文件中也是 [有好处](http://www.jonathanklein.net/2014/02/revisiting-cookieless-domain.html) 的，有时甚至比缓存和内联更为有效。 Chrome 请求这个页面的时候会再发送一个 HTTP 连接到根目录，从而不需要 TCP 连接来获取这个 CSS。（感谢 Philip！）
    
    需要注意的一些问题是：和 `preload` 不同的是，preload 可以触发来自任何域的预加载，而你只能从你自己的域或你所授权的域中推送资源。 一旦服务器得到来自客户端的第一个请求，就可以启动它。 服务器将资源压入缓存，并在连接终止时被删除。 但是，由于可以在多个选项卡之间重复使用 HTTP/2 连接，所以推送的资源也可以被来自其他选项卡的请求声明。（感谢 Inian！）
    
    目前，服务器并没有一个简单的方法得知被推送的资源是否已经存在于 [用户的缓存中](https://blog.yoav.ws/tale-of-four-caches/)，因此每个用户的访问都会继续推送资源。因此，您可能需要创建一个缓存 [监测 HTTP/2 服务器推送机制](https://css-tricks.com/cache-aware-server-push/)。如果被提取，您可以尝试从缓存中获取它们，这样可以避免再次推送。
    
    但请记住，[新的 cache-digest 规范](https://calendar.perfplanet.com/2016/cache-digests-http2-server-push/) 无需手动建立这样的 **缓存感知** 的服务器，基本上在 HTTP/2 中声明的一个新的帧类型就可以表达该主机的内容。因此，它对于 CDN 也是特别有用的。
    
    对于动态内容，当服务器需要一些时间来生成响应时，浏览器无法发出任何请求，因为它不知道页面可能引用的任何子资源。 在这种情况下，我们可以预热连接并增加 TCP 拥塞窗口大小，以便将来的请求可以更快地完成。 而且，所有内联配置对于服务器推送都是较好的选择。事实上，Inian Parameshwaran [对 HTTP/2 Push 和 HTTP Preload 进行了比较 深入的研究](https://dexecure.com/blog/http2-push-vs-http-preload/)，内容很不错，其中包含了您可能需要的所有细节。服务器到底是推送还是不推送呢？你可以阅读一下 Colin Bendell 的 [Should I Push？](https://shouldipush.com/)。可能会给你指出正确的方向。
    
    一句话：正如 Sam Saccone [所说](https://medium.com/@samccone/performance-futures-bundling-281543d9a0d5)，`preload` 有利于将资源的开始下载时间更接近初始请求， 而服务器推送是一个完整的 RTT（或 [更多](https://blog.yoav.ws/being_pushy/)，这取决于您的服务器反应时间） —— 如果你有一个服务器可以防止不必要的推送。

43. **尝试重新组合 CSS 规则**

    我们经常要使用到关键的 CSS，但是还有一些优化可以做得更好。哈里·罗伯茨进行了[一项引人注目的研究](https://csswizardry.com/2018/11/css-and-network-performance/)，得出了相当惊人的结果。例如，将主CSS文件拆分为独立的媒体查，这样，浏览器将检索具有高优先级的关键CSS，然后把具有低优先级的其他所有内容分离到非关键CSS当中。
    
    此外，避免 `<link rel="stylesheet" />` 在 `async` 代码片段之前放置。如果一个脚本不依赖于任何样式表，可以考虑将独立脚本放在独立样式之上。如果是这样，我们可以将这个脚本分割成一个单独的模块，并将其加载到 CSS 的任何一侧。
    
    Scott Jehl 通过 [使用 service worker 缓存内联CSS文件](https://www.filamentgroup.com/lab/inlining-cache.html) 解决了另一个有趣的问题。基本上，我们在 `style` 元素上添加一个 `ID` 属性，以便使用 `JavaScript` 快速引用，然后一小段 `JavaScript` 找到目标 CSS 并使用 Cache API 将其存储在本地浏览器缓存中（内容类型为 `text/css`），以便在后续页面上使用。所以我们为了避免在后续页面上引用内联 CSS 并在外部引用缓存资产，就会在第一次访问站点时设置 cookie。
    
    ![]()
    你使用 [流响应](https://jakearchibald.com/2016/streams-ftw/) 吗？通过流，在初始导航请求中呈现的 HTML 可以充分利用浏览器的流式 HTML 解析器。

44. **流响应**

    [streams](https://streams.spec.whatwg.org/) 经常被遗忘和忽略，它提供了异步读取或写入数据块的接口，在任何给定的时间内，只有一部分数据可能在内存中可用。基本上，只要第一个数据块可用，它们就允许原始请求的页面开始处理响应，并使用针对流进行优化的解析器逐步显示内容。
    
    我们可以从多个源创建一个流。例如，您可以让 service worker 构建一个 streams，其中框架 （shell）来自缓存，内容来自网络的流，而不是提供一个空的 UI 外壳并让JavaScript填充它。正如 Jeff Posnick [指出的](https://developers.google.com/web/updates/2016/06/sw-readablestreams)，如果您的 web 应用程序由 CMS 提供支持的，那么服务器渲染 HTML 是通过将部分模板拼接在一起来呈现的，该模型将直接转换为使用流式响应，而模板逻辑将从服务器复制而不是你的服务器。Jake Archibald 的 [The Year of Web Streams](https://jakearchibald.com/2016/streams-ftw/) 文章重点介绍了如何构建它。对于性能的提升是[非常明显](https://www.youtube.com/watch?v=Cjo9iq8k-bc)。
    
    流化整个 HTML 响应的一个重要优点是，在初始导航请求期间呈现的HTML可以充分利用浏览器的流化HTML解析器。加载页面后插入文档的 HTML 块(通过 JavaScript 填充的内容很常见)不能利用这种优化。
    流式传输整个 HTML 响应的一个重要优点是，在初始导航请求期间呈现的 HTML 可以充分利用浏览器的流式 HTML 解析器。但是在页面加载之后插入到文档中的 HTML 块（与通过 JavaScript 填充的内容一样常见）无法利用此优化。
    
    浏览器支持程度如何呢？[使用](https://caniuse.com/#search=streams) Chrome 52 +，Firefox 57+，Safari 和 Edge，[支持所有现代浏览器](https://caniuse.com/#search=serviceworker) 支持的API和 service worker。

45. **考虑使组件连接/设备内存感知**
    
    特别是在新兴市场工作时，你可能需要考虑优化用户选择节省数据的体验。[保存数据客户端提示请求头](https://developers.google.com/web/updates/2016/02/save-data) 允许我们为成本和性能受限的用户定制应用程序和有效载荷。实际上，您可以 [将高DPI图像的请求重写为低DPI图像](https://css-tricks.com/help-users-save-data/)，删除Web字体和花哨的特效，预览缩略图和无限滚动，关闭视频自动播放，服务器推送，减少显示项目数量，降低图像质量，甚至更改 [提供标记的方式](https://dev.to/addyosmani/adaptive-serving-using-javascript-and-the-network-information-api-331p)。Tim Vereecke 发表了一篇关于 [Data-s(h)aver 策略](https://calendar.perfplanet.com/2018/data-shaver-strategies/) 的详细文章，其中包含许多 Data-saver 选项。
    
    该头部目前仅支持 Chromium，Android 版 Chrome 或 桌面设备上的 Data Saver 扩展。当然，您还可以使用 [Network Information API](https://googlechrome.github.io/samples/network-information/) 根据网络类型交付 [低/高分辨率的图像](https://justmarkup.com/log/2017/11/network-based-image-loading/) 和视频。网络信息API 和 `navigator.connection.effectiveType` (Chrome 62+)，都是使用 `RTT` 值、下行（`downlink`）值、有效类型（`effectiveType`）值(和其他一些值)来表示连接和用户可以处理的数据。
    
    在这种情况下，Max Stoiber 谈到了 [连接感知组件](https://mxb.at/blog/connection-aware-components/)。例如，使用 React，我们编写一个组件，在不同的渲染方式下可能会加载成不同的元素。Max建议，一个 `<Media />` 组件在新闻板块的输出可能会出现情况：
    - `Offline`：带 `alt` 文本的占位符
    - `2G` / `save-data` mode：低分辨率图像
    - `3G` 在非Retina屏幕上：中等分辨率图像
    - `3G` 在Retina屏幕上：高分辨率Retina图像
    - `4G` 高清视频
    
    Dean Hume使用service worker提供了一个 [类似逻辑的实际实现](https://deanhume.com/dynamic-resources-using-the-network-information-api-and-service-workers/)。对于视频，我们可以默认显示一个视频海报，然后在更好的连接上显示 **播放** 图标以及视频播放器外壳、视频的元数据等。对于不支持的浏览器，我们可 [以侦听`canplaythrough`事件](https://benrobertson.io/front-end/lazy-load-connection-speed)，如果 `canplaythrough` 事件在 2s 内没有触发，则使用 `Promise.race()` 来超时加载资源。

46. **考虑使您的组件设备具有内存感知能力**

    网络连接只是为用户提供了一个视口。如果想更进一步，您还可以使用 [Device Memory API](https://developers.google.com/web/updates/2017/12/device-memory)（Chrome 63+）[根据可用的设备内存动态调整资源](https://calendar.perfplanet.com/2018/dynamic-resources-browser-network-device-memory/)。返回设备有多少RAM（千兆字节），向下舍入到最接近的2的幂。`navigator.deviceMemory` 返回设备的RAM大小（千兆字节），四舍五入到最接近的2次方。该API还具有一个客户端提示头，`Device-Memory`，并且给出相同的值。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/20/1686a4fc11045cc7?w=1600&h=542&f=gif&s=9685894)
    DevTools 中的 **Priority** 列。图片来源：Ben Schwarz，重要的请求

47. **预热连接以加快传输速度**

    使用 [资源提示](https://w3c.github.io/resource-hints/) 来节约时间，如 [dns-prefetch](https://caniuse.com/#search=dns-prefetch)（在后台执行 DNS 查询），[preconnect](https://www.caniuse.com/#search=preconnect)（告诉浏览器在后台进行连接握手（DNS, TCP, TLS）），[prefetch](https://caniuse.com/#search=prefetch)(告诉浏览器请求一个资源) 和 [preload](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)(预先获取资源而不执行他们)。
    
    大多数时候，我们至少会使用 `preconnect` 和 `dns-prefetch`，我们会小心使用 `prefetch` 和 `preload`；前者只能在你非常确定用户后续需要什么资源的情况下使用（类似于采购渠道）。注意，`prerender` 已被弃用，不再被支持。
    
    请注意，即使使用 `preconnect` 和 `dns-prefetch`，浏览器也会对它将并行查找或连接的主机数量进行限制，因此最好是将它们根据优先级进行排序（感谢 Philip！）。
    
    事实上，使用资源提示可能是最简单的提高性能的方法，[它确实很有效](https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf)。什么时候该使用呢？Addy Osmani已经做了 [解释](https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf)，我们应该预加载确定将在当前页面中使用的资源。预获取可能用于未来页面的资源，例如用户尚未访问的页面所需的 Webpack 包。
    
    Addy 的 [关于 Chrome 中加载优先级](https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf) 的文章展示了Chrome 是如何精确地解析资源提示的，因此一旦你决定哪些资源对页面渲染比较重要，你就可以给它们赋予比较高的优先级。你可以在 Chrome DevTools 网络请求表格（或者 Safari Technology Preview）中启动 `priority` 列来查看你的请求的优先级。
    
    例如，由于字体通常是页面上的重要资源，所以最好[使用 `preload` 请求浏览器下载字体](https://css-tricks.com/the-critical-request/#article-header-id-2)。你也可以 [动态加载 JavaScript](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/#dynamic-loading-without-execution)，从而有效的执行延迟加载。同样的，因为 `<link rel="preload">` 接收一个 `media` 属性，你可以基于媒体查询规则来 [有选择性地优先加载资源](https://css-tricks.com/the-critical-request/#article-header-id-3)。
    
    [需要注意的一些问题](https://dexecure.com/blog/http2-push-vs-http-preload/)是：`preload` 可以将 [资源的下载时间](https://www.youtube.com/watch?v=RWLzUnESylc) 移到请求开始时，但是这些缓存在内存中的预先加载的资源是绑定在所发送请求的页面上，也就是说预先加载的请求不能被页面所共享。而且，`preload` 与 HTTP 缓存配合得也很好：如果缓存命中则不会发送网络请求。
    
    因此，它对后发现的资源也非常有用，如：通过 `background-image` 加载的一幅 hero image，内联关键 CSS （或 JavaScript），并预先加载其他 CSS （或 JavaScript）。
    此外，只有当浏览器从服务器接收 HTML，并且前面的解析器找到了 `preload` 标签后，`preload` 标签才可以启动预加载。
    
    由于我们不等待浏览器解析 HTML 以启动请求，所以通过 HTTP 头进行预加载要快一些。[Early Hints](https://www.fastly.com/blog/faster-websites-early-priority-hints) 将进一步提供帮助，甚至可以在发送HTML的响应标头之前启用预加载，而 [Priority Hints](https://github.com/WICG/priority-hints)（[即将推出](https://www.chromestatus.com/feature/5273474901737472)）将帮助我们指示脚本的加载优先级。
    
    请注意：如果你正在使用 `preload`、`as` **必须**定义，否则[什么都不会加载](https://twitter.com/yoavweiss/status/873077451143774209)；还有，预加载字体时如果没有 `crossorigin` 属性将会获取两次。

48. **使用 Service workers 进行缓存和网络回退**

    网络上的任何性能优化都不会比用户计算机上的本地存储缓存更快。如果您的网站是通过 HTTPS 运行的，请使用 **[Service Workers 实用指南](https://github.com/lyzadanger/pragmatist-service-worker)** 将静态资源缓存在 service worker 缓存中，并存储脱机回退(甚至离线页面)，然后从用户的计算机中检索它们，而不是转到网络。另外，查看 Jake 的 [Offline Cookbook](https://jakearchibald.com/2014/offline-cookbook/) 和免费的 Udacity课程 [离线Web应用程序](https://cn.udacity.com/course/offline-web-applications--ud899)。
    
    浏览器支持吗？如上所述，[它得到了广泛的支持](https://caniuse.com/#search=serviceworker)(Chrome、Firefox、Safari TP、三星互联网、Edge 17+)，无论如何，网络是它的退路。它有助于提高性能吗？[是的](https://developers.google.com/web/showcase/2016/service-worker-perf)，而且它正在变得更好，例如使用Background Fetch允许service worker进行后台上传/下载，[运送到Chrome 71](https://groups.google.com/a/chromium.org/forum/#!msg/blink-dev/z5WX-2RMulo/JQqeF3XZAgAJ)。
    
    service worker有许多用例。例如，您可以 [实现 **保存为脱机** 特性](https://una.im/save-offline/#%F0%9F%92%81)，[处理损坏的图像](https://bitsofco.de/handling-broken-images-with-service-worker/)，[在选项卡之间引入消息传递](https://www.loxodrome.io/post/tab-state-service-workers/)，或者 [根据请求类型提供不同的缓存策略](https://medium.com/dev-channel/service-worker-caching-strategies-based-on-request-types-57411dd7652c)。通常，一种常见的可靠策略是将应用程序 shell 与一些关键页面一起存储在 service worker 的缓存中，例如离线页面、首页和其他可能对您的应用程序很重要的页面。
    
    但是要记住一些问题。在有了service worker之后，我们需要 [在Safari中提防范围请求](https://philna.sh/blog/2018/10/23/service-workers-beware-safaris-range-request/)（如果您正在为服务工作者使用 Workbox，它有一个范围请求模块）。如果您偶然发现控台出现 `DOMException:Quota exceeded.` 这样的错误提示，那么请查看 Gerardo 的文章 [当7KB等于7MB时](https://cloudfour.com/thinks/when-7-kb-equals-7-mb/)。
    
    正如 Gerardo 所写的一样，如果您正在构建一个渐进式Web应用程序，并且当您的 service worker 缓存来自 CDN 的静态资源时，这时候您的缓存存储空间会非常大。所以请确保对于跨源资源 [存在正确的 CORS 响应头](https://cloudfour.com/thinks/when-7-kb-equals-7-mb/#opaque-responses)，这样您就不会在无意中使用 Service Workers [缓存不透明的响应](https://cloudfour.com/thinks/when-7-kb-equals-7-mb/#should-opaque-responses-be-cached-at-all)，您还可以向 `< img >` 标记添加 `crossorigin` 属性来 [选择将跨源图像资源缓存到 CORS 模式中](https://cloudfour.com/thinks/when-7-kb-equals-7-mb/#opt-in-to-cors-mode)。
    
    使用 service worker 的一个很好的起点是 [Workbox](https://developers.google.com/web/tools/workbox/)，这是一组专门用于构建渐进式 Web 应用程序的 service worker 库。

49. **您是否使用 CDN / Edge 上的 Service workers（例如，进行A / B测试）**

    这时候，我们已经习惯于在客户端上运行 Service workers，但是随着 [CDNs 在服务器上实现它们](https://blog.cloudflare.com/introducing-cloudflare-workers/)，我们还可以使用它来调整边缘性能。
    
    例如，在A / B测试中，当 `HTML` 需要为不同用户改变其内容时，我们可以 [使用 CDN 服务器上的 Service Workers](https://www.filamentgroup.com/lab/servers-workers.html) 来处理逻辑。我们还可以对 [HTML 重写](https://twitter.com/patmeenan/status/1065567680298663937) 进行 [流式处理](https://twitter.com/patmeenan/status/1065567680298663937)，以加快使用 Google 字体的网站的速度。

50. **您是否优化了渲染性能**

    使用 [CSS containment](https://caniuse.com/#search=contain) 隔离昂贵的组件 - 例如，限制浏览器样式、用于非画布导航的布局和绘画工作，第三方组件的范围。确保在滚动页面没有延迟，或者当一个元素进行动画时，持续地达到每秒 60 帧。如果这是不可能的，那么至少要使每秒帧数持续保持在 60 到 15 的范围。使用 [CSS 的 will-change](https://caniuse.com/#feat=will-change) 通知浏览器哪个元素的哪个属性将要发生变化。
    
    此外，评估 [运行时渲染性能](https://aerotwist.com/blog/my-performance-audit-workflow/#runtime-performance)（例如，使用 [DevTools](https://developers.google.com/web/tools/chrome-devtools/rendering-tools/)）。可以通过学习 Paul Lewis 的 [关于浏览器渲染优化](https://cn.udacity.com/course/browser-rendering-optimization--ud860)的 Udacity 课程（免费）和 Georgy Marchuk [关于浏览器绘制和web性能注意事项](https://css-tricks.com/browser-painting-and-considerations-for-web-performance/) 的文章。
    
    如果你想更深入地了解这个主题，Nolan Lawson 分享了一篇文章叫做 [准确测量布局性能的技巧](https://nolanlawson.com/2018/09/25/accurately-measuring-layout-on-the-web/)，而 Jason Miller 也给出了一个建议 [替代的技术](https://twitter.com/_developit/status/1081682550865752064)。同样，我们还有一篇由 Sergey Chikuyonok 写的关于 [如何正确使用 GPU 动画](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/) 的文章。注意：对 GPU-composited 层的更改是[代价最小](https://blog.algolia.com/performant-web-animations/) 的，如果你能通过 `opacity` 和 `transform` 来触发合成，那么你就是在正确的道路上。Anna Migas 在她关于 [调试UI渲染性能](https://vimeo.com/302791098) 的演讲中也提供了很多实用的建议。

51. **您是否优化了渲染体验**

    组件以何种顺序显示在页面上以及我们如何给浏览器提供资源固然重要，但是我们也不应该低估了 [感知性能](https://www.smashingmagazine.com/2015/09/why-performance-matters-the-perception-of-time/) 的作用。这一概念涉及到等待的心理学，主要是让用户在其他事情发生时保持忙碌。这就涉及到了 [感知管理](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/)，[优先开始](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#preemptive-start)，[提前完成](https://www.smashingmagazine.com/2015/11/why-performance-matters-part-2-perception-management/#early-completion) 和 [宽容管理](https://www.smashingmagazine.com/2015/12/performance-matters-part-3-tolerance-management/)。
    
    这一切意味着什么？在加载资源时，我们可以尝试始终领先于客户一步，所以将很多处理放置到后台，响应会很迅速。让客户参与进来，我们可以用 [骨架屏幕（实例演示）](https://twitter.com/lukew/status/665288063195594752)，而不是当没有更多优化可做时，用加载指示或者添加一些动画/过渡来 [欺骗用户体验](https://blog.stephaniewalter.fr/en/cheating-ux-perceived-performance-and-user-experience/)。但是要注意：在部署之前应该对骨架屏幕进行测试，因为一些 [测试显示](https://www.viget.com/articles/a-bone-to-pick-with-skeleton-screens/)，从所有指标来看，骨架屏幕的 [性能是最差的](https://www.viget.com/articles/a-bone-to-pick-with-skeleton-screens/)。

### HTTP/2

52. **迁移到HTTPS，然后打开HTTP / 2**

    随着 [Google 向更安全的网络发展](https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html)，并最终将 Chrome 中的所有 HTTP 网页认定为 **不安全** 的大环境下，迁移到 [HTTP / 2环境](https://http2.github.io/faq/) 是不可避免的。[HTTP / 2 从目前来看得到很好的支持](https://caniuse.com/#search=http2)， 而且，在大多数场景下，使用 HTTP/2 会让你大力出奇。一旦在 HTTPS 上运行，您可以在 service workers 和 server push 方面得到 [显著的性能提升](https://www.youtube.com/watch?v=RWLzUnESylc&t=1s&list=PLNYkxOF6rcIBTs2KPy1E6tIYaWoFcG3uj&index=25)。
    
    ![](https://user-gold-cdn.xitu.io/2019/1/19/16861b2abdae1a8e?w=1600&h=776&f=png&s=53729)
    最终，谷歌计划将所有 HTTP 页面标记为不安全的，并将有问题的 HTTPS 的 HTTP 安全指示器更改为红色三角形。
    
    最耗时的任务是 [迁移到 HTTPS](https://https.cio.gov/faq/)，不过这取决于你的 HTTP/1.1 用户量有多大（即使用旧版操作系统或浏览器的用户），你将不得不为旧版的浏览器性能优化发送不同的构建版本，这需要你采用 [不同的构建流程](https://rmurphey.com/blog/2015/11/25/building-for-http2)。注意：开始迁移和新的构建过程可能会很棘手，而且耗费时间。接下来所讲的内容，都是针对之前切过 HTTP/2 环境或者现在正准备切 HTTP/2 环境（的读者）来展开的。

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

