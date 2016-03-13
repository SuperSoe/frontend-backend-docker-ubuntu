## spring controller单元测试遇到的问题#
*由于ｓｐｒｉｎｇ的依赖注入的问题，单元测试开始前，需要将需要注入的注入*
`ReflectionTestUtils.setField(wifiController, "soeUserService", soeUserService);`
`ReflectionTestUtils.setField(需要注入的目标, "注入对象名称", 注入对象);`