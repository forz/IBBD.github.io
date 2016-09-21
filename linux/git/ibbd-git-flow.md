# IBBD Git开发流程规范

本规范适合多人合作开发的流程，小的产品或者项目可以不遵守该规范。

## 规范流程图

![IBBD Git规范流程图](/_img/IBBD-Git开发流程规范.png)

说明：

将项目的开发过程分成开发，测试，上线三个阶段的迭代过程，分别对应开发，测试和运维的相关同事；对应到git上，开发同事主要在Master分支上开发，测试同事只对release分支进行测试，而运维的同事则从release分支生成tag，并将tag部署到生产环境中。

## 开发

- 基于master分支进行开发。
- 里程碑开发完成（通过了开发自己的测试是基本的要求），则将master分支合并到release分支并push到远程，然后在测试服务器pull最新的release分支，再告知测试的同事（或者是项目负责人，由负责人来协调）进行测试。
- 测试的同事在测试期间，开发的同事切换回master分支，继续开发下一个里程碑的版本。
- 需要bug fix的时候，切换到release分支（这时不能合并master分支到release分支），fix之后，再切换回master分支，这时需要将release分支合并回master分支，此时应该同步master分支的代码，避免引起冲突。最后，记得关闭相关的Issue。

## 测试

- 在开始一个里程碑版本的测试时，将发现的问题记录到Issue中。
- 一轮测试完成之后，告知开发的同事进行fix。
- 待开发的同事将Issue列表都修复关闭之后，检查是否真的应该完成了修复，如果发现还有问题，则Reopen相应的Issue。
- Issue确认都没有问题之后，告知运维的同事进行上线。
- 生产环境上线之后，测试的同事也应该跟进做一轮测试，避免在正式环境上存在重大问题。

## 运维

- 在release分支测试ok之后，开始git tag，并推送到远程。
- 在生产服务器pull相应的tag，如果有多台服务器，则可以先上线一台（如果可以的话）
- 上线之后注意观察服务器的各项指标是否正常，如果不正常，则属于紧急问题，切换回上一个正常的tag，并提Issue，告知开发优先修复。修复完成后，经过测试ok后，重新上线。
- 最后，没问题才能完成上线。

## 附：IBBD Issue使用规范

![IBBD Issue使用规范](/_img/IBBD-Issue使用规范.png)

