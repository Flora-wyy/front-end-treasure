### 什么是monorepo
Monorepo 的全称是 monolithic repository，即单体式仓库，与之对应的是 Multirepo(multiple repository)，这里的“单”和“多”是指每个仓库中所管理的模块数量。

Multirepo 是比较传统的做法，即每一个 package 都单独用一个仓库来进行管理。例如：Rollup, ...

Monorep 是把所有相关的 package 都放在一个仓库里进行管理，每个 package 独立发布。 例如：React, Angular, Babel, Jest, Umijs, Vue ...


package之间相互依赖，开发人员需要在本地手动执行npm link，维护版本号的更替；
issue难以统一追踪，管理，因为其分散在独立的repo里；
每一个package都包含独立的node_modules，而且大部分都包含babel,webpack等开发时依赖，安装耗时冗余并且占用过多空间。

### 有哪些库 
lerna 
pnpm  当使用 npm 或 Yarn 时，如果你有 100 个项目，并且所有项目都有一个相同的依赖包，那么， 你在硬盘上就需要保存 100 份该相同依赖包的副本。然而，如果是使用 pnpm，依赖包将被 存放在一个统一的位置
yarn

性能差（Bad performance）：单一代码库难以扩大规模，像git blame这样的命令可能会不合理的花费很长时间执行，IDE也开始变得缓慢，生产力受到影响，对每个提交测试整个repo变得不可行。
破坏主线（Broken main/master）：主线损坏会影响到在单一代码库中工作的每个人，这既可以被看作是灾难，也可以看作是保证测试既可以保持简洁又可以跟上开发的好机会。
学习曲线（Learning curve）：如果代码库包含了许多紧密耦合的项目，那么新成员的学习曲线会更陡峭。
大量的数据（Large volumes of data）：单一代码库每天都要处理大量的数据和提交。
所有权（Ownership）：维护文件的所有权更有挑战性，因为像Git或Mercurial这样的系统没有内置的目录权限。
Code reviews：通知可能会变得非常嘈杂。例如，GitHub有有限的通知设置，不适合大量的pull request和code review。