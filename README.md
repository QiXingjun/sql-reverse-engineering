# sql_reverse_engineering

## 数据库逆向工程

本段代码实现由数据库文件（sql文件）来生成Java Mapper和POJO文件。

注意：想要重新生成的话，需要将第一次生成的文件删除，因为第二次生成的文件不会覆盖第一次生成的问价，而是会在后面进行添加。

还有，要注意修改generatorConfig.xml文件中的一些配置：

```java
<generatorConfiguration>
	<context id="testTables" targetRuntime="MyBatis3">
		<commentGenerator>
			<!-- 是否去除自动生成的注释 true：是 ： false:否 -->
			<property name="suppressAllComments" value="true" />
		</commentGenerator>
		<!--数据库连接的信息：驱动类、连接地址、用户名、密码  注意此处要将驱动类、连接地址、用户名、密码换成自己的 -->
		<jdbcConnection driverClass="com.mysql.jdbc.Driver"
			connectionURL="jdbc:mysql://localhost:3306/school2shou" userId="root"
			password="root">
		</jdbcConnection>
		<!-- 默认false，把JDBC DECIMAL 和 NUMERIC 类型解析为 Integer，为 true时把JDBC DECIMAL 和 
			NUMERIC 类型解析为java.math.BigDecimal -->
		<javaTypeResolver>
			<property name="forceBigDecimals" value="false" />
		</javaTypeResolver>

		<!-- targetProject:生成PO类的位置  注意此处要将生成PO类的位置换成自己的 -->
		<javaModelGenerator targetPackage="com.school2shou.pojo"
			targetProject=".\src">
			<!-- enableSubPackages:是否让schema作为包的后缀 -->
			<property name="enableSubPackages" value="false" />
			<!-- 从数据库返回的值被清理前后的空格 -->
			<property name="trimStrings" value="true" />
		</javaModelGenerator>
        <!-- targetProject:mapper映射文件生成的位置 注意此处要将mapper映射文件生成的位置换成自己的-->
		<sqlMapGenerator targetPackage="com.school2shou.mapper" 
			targetProject=".\src">
			<!-- enableSubPackages:是否让schema作为包的后缀 -->
			<property name="enableSubPackages" value="false" />
		</sqlMapGenerator>
		<!-- targetPackage：mapper接口生成的位置 注意此处要将mapper接口生成的位置换成自己的-->
		<javaClientGenerator type="XMLMAPPER"
			targetPackage="com.school2shou.mapper" 
			targetProject=".\src">
			<!-- enableSubPackages:是否让schema作为包的后缀 -->
			<property name="enableSubPackages" value="false" />
		</javaClientGenerator>
		<!-- 指定数据库表 注意填写自己想要进行逆向的数据库表-->
		<table schema="" tableName="tb_item"></table>
	</context>
</generatorConfiguration>
```
