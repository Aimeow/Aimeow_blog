title: 用鸡讲解技术债务的形成过程
date: 2015-06-08 15:38:13
tags:
---
技术债务，是指在面对需求时，由于仓促地实现某些功能特性而对代码库产生了破坏（同时，在此过程中破坏了代码库的架构设计）。对于一 些经理或客户来说技术债务仿佛是一个陌生的概念。也许他们知道，只是他们不太想听，我不确定。不管怎样，我想到了一个小故事，在下次某些新的特性需求提出 时，我会用这个故事告诉他们实现这些特性的代价有多大。

　　有一个农民，他有三只鸡，每只鸡每天生一个蛋。农民与当地的一个杂货店有生意来往。杂货商每天从农民那里买两个鸡蛋，这样他可以在他的店里出售。一切都有条不紊地进行着，直到有一天杂货商出现在农民的家门口。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>嘿，今天我想要一些鸡肉。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>肉吗？这可不在我们约定的协议范围之内。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>我知道，但我真的需要肉。这是为我计划的一个企业家禽服务平台做准备的。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>什么？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>一些重要人物。你能给我一些吗？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>嗯…这不那么容易，我必须孵化鸡蛋然后等待雏鸡长大。我认为这需要一个月左右的时间。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>一个月？时间太长了…我更喜欢现在就拿到。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>大自然有其自身的规律，你必须等待一段时间。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>嗯…为什么你不杀一只鸡呢？这样一来，我将得到我想要的肉，你仍然可以每天生产两个鸡蛋。事实上你每天也不需要更多的鸡蛋，不是吗？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>嗯…我不认为这是一个好主意。当其它的鸡发生一些意外的状况时，这会让我陷入困境，可能无法提供两个鸡蛋。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>来吧，不会有什么事情发生的…况且，我真的，真的需要肉！你能给我吗？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>好吧，我想我可以…

　　说完，农民拿起屠刀将其中的一只鸡送到了造物主那。杂货商拿着他的肉回到了他的店里。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>嘿！

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>嘿，怎么啦？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>听着，上次的肉很好。事实上，它真的很美味，而且卖得非常好。所以现在，也就是明天之前，我至少要拿到一只鸡。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>这是不可能的。如果我给你另一只鸡，我就无法按照合约里面的条款每天供应两个鸡蛋了。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>哎呀，快点啦。客户想要肉，而且我已经答应了明天一定会提供肉的…

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>不，我不能这样做。如果我这样做，我就不能履行合同，你明白吗？如果我这样做了，鸡蛋就不能保证。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>但是我真的，真的，真的需要肉！就在明天！否则客户会生气，地球会毁灭，整个世界正如我们所知道的那样会结束！给我一只鸡，现在！

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>嗯…如果你真的很想要，那你拿走吧！但是我要再次提醒你，从现在开始，我无法保证每天有足够的鸡蛋。明白吗？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>当然了，这我知道的。但是你是一个聪明的家伙，我想无论如何你会想出办法解决这个问题的。拜拜！

　　杂货商走了，再次回到了他的店铺。

　　一天后：

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>你好！鸡蛋出什么问题了？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>你是指什么？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>鸡蛋，就是指鸡蛋，怎么只有一个鸡蛋？出什么问题了？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>出什么问题了？我有三只鸡，你拿走了两只，现在，这里只有一只鸡。一只鸡下一个鸡蛋，我想这是很清楚的事情。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>但是合约中没有这些！合同规定的条款就摆在这里。你每天欠我两个鸡蛋！现在你要我怎么向我的客户解释？

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">农民：</span>嗯，对此我是非常清楚的，而且我也无能为力。

　　<span style="font-weight:bold;color:#9900cc;font-size:120%;">杂货商：</span>好吧，好吧，天哪，算了吧，说的别的吧…如果能再拿一些肉走那还不错，我能拿走一些吗？

　　所以，不要当一个农民。当需求来时，拒绝可能对你的代码库造成无法挽回的破坏的需求，一旦你被强迫去做这样的事情，绝对不要对已被破坏的残骸负责。同样，不要当一个杂货商—不要要求一些不可能完成的任务，同时为自己的决定承担责任。

　　PS：在写这篇博文时没有任何的鸡受到伤害 ^o^

-----------------------
http://www.cnbeta.com/articles/176702.htm