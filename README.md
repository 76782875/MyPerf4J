# MyPerf4J
一个简单、快速的Java接口性能监控和统计工具

## 背景
* 我需要一个能统计接口响应时间的程序
* perf4j现有的统计数据不能满足我的需求

## 需求
* 能统计出接口的RPS、TP50、TP90、TP95、TP99等性能指标
* 可以通过注解进行配置，注解可以配置到类和/或接口上，并可以通过参数配置调优内存占用
* 尽量不占用过多的内存、不影响程序的正常响应
* 性能指标的处理可以定制化，例如：日志收集、上报给日志收集服务等

## 设计
* 通过把所有的响应时间记录下来，便可以进行所有可能的分析，包括RPS、TP99等，那么如何高效的存储这些数据呢？
    - 采用K-V的形式即可，K为响应时间，V为对应的次数，这样内存的占用只和不同响应时间的次数有关，而和总请求次数无关
    - 核心数据结构为数组+Map，根据二八定律，绝大多数的接口相应时间在很小的范围内，这个很小的范围特别适合使用数组来存储；而少数的接口响应时间分布的范围则会比较大，适合用Map来存储
* 利用AOP进行响应时间的采集
* 异步处理采集结果，避免影响接口的正常响应
* 把处理采集的结果的接口暴露出来，方便进行自定义的处理

## 进度
* 核心数据结构开发完成
* AOP相关功能开发完成
* 性能指标统计功能开发完成

