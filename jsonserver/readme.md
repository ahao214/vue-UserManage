// 获取所有用户信息
http://localhost:3000/users

// 获取id为1的用户信息
http://localhost:3000/users/1

// 获取所有company信息
http://localhost:3000/companies

// 获取单个公司的信息
http://localhost:3000/companies/1

// 获取公司id为3的所有员工
http://localhost:3000/companies/3/users

// 根据公司名字获取公司信息
http://localhost:3000/companies?name=apple

// 根据多个名字获取公司信息
http://localhost:3000/companies?name=apple&name=google

// 获取一页中只有2条数据
http://localhost:3000/companies?_page=1&_limit=2

// 实现对数据的排序-升序排序
http://localhost:3000/companies?_sort=name&_order=asc

// 获取年龄为30以上的人眼
http://localhost:3000/users?age_gte=30

// 获取年龄在30到40之间
http://localhost:3000/users?age_gte=30&age_gte=40

// 根据搜索信息来查询
http://localhost:3000/users?q=emily



