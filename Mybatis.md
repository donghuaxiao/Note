<style type="text/css">
code {
	color:blue;
	font-size: 14px;
}
</style>

## Mybatis 教程

### for-each

* item ：循环体重的具体对象。 支持属性的点路径访问，如item.age, item.info.detail 
   具体说明： 在list 和数组中是其中的对象，在map中是value, 该参数为必须|
* collection: 要迭代的对象, 作为传人参数，List<?> 对象默认使用list 代替作为键，数组对象有array代替作为键， Map对象没有默认的键。 在作为传入参数时可以使用@Param("keyName")来设置键， 设置keyName后， list,array将会失效。该参数为必须
* separator: 元素之间的分割符， 例如，在in() 的时候， separtor=",", 该参数为可选.
* open： foreach代码的开始符号，一般是(, 和 close=")"结合使用，常用在in(), values()时， 该参数为可选。
* close： foreach代码的结束符号， 一般是), 该参数为可选。
* index: 在 list 和 数组中，index 是元素的符号， 在map 中， index 是元素的key, 该参数为可选参数。

例子：
生成sql 语句： select * from users where user in ( id1, id2)

	<select id="listUsers" resultType="userType" paramterType="list">
		select *　from users 
		<where>
			id in
			<foreach item="user" collection="list" separator="," open="(", close=")", index="">
				#{item.id, jdbcType=NUMERIC}
			</foreach>
		</where>
	</select>