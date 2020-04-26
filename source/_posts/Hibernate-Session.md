---
title: Hibernate Session
date: 2017-02-20 00:25:55
tags: [Hibernate, JPA]
categories: [Dev, Hibernate]
---

![hibernate](https://philsblog.b-cdn.net/images/hibernate.jpeg "hibernate")

States:
* Transient
* Persistent
* Detached

# A typical sample of tranction
```Java
Session session = factory.openSession();
Transaction tx = null;
try {
   tx = session.beginTransaction();
   // do some work
   ...
   tx.commit();
}
catch (Exception e) {
   if (tx!=null) tx.rollback();
   e.printStackTrace(); 
}finally {
   session.close();
}
```

# Session interface
|Method|Description|
|:-|:-|
|Transaction beginTransaction()|开始工作单位，并返回关联事务对象。|
|void cancelQuery()|取消当前的查询执行。|
|void clear()|完全清除该会话。|
|Connection close()|通过释放和清理 JDBC 连接以结束该会话。|
|Criteria createCriteria(Class persistentClass)|为给定的实体类或实体类的超类创建一个新的 Criteria 实例。|
|Criteria createCriteria(String entityName)|为给定的实体名称创建一个新的 Criteria 实例。|
|Serializable getIdentifier(Object object)|返回与给定实体相关联的会话的标识符值。|
|Query createFilter(Object collection, String queryString)|为给定的集合和过滤字符创建查询的新实例。|
|Query createQuery(String queryString)|为给定的 HQL 查询字符创建查询的新实例。|
|SQLQuery createSQLQuery(String queryString)|为给定的 SQL 查询字符串创建 SQLQuery 的新实例。|
|void delete(Object object)|从数据存储中删除持久化实例。|
|void delete(String entityName, Object object)|从数据存储中删除持久化实例。|
|Session get(String entityName, Serializable id)|返回给定命名的且带有给定标识符或 null 的持久化实例（若无该种持久化实例）。|
|SessionFactory getSessionFactory()|获取创建该会话的 session 工厂。|
|void refresh(Object object)|从基本数据库中重新读取给定实例的状态。|
|Transaction getTransaction()|获取与该 session 关联的事务实例。|
|boolean isConnected()|检查当前 session 是否连接。|
|boolean isDirty()|该 session 中是否包含必须与数据库同步的变化？|
|boolean isOpen()|检查该 session 是否仍处于开启状态。|
|Serializable save(Object object)|先分配一个生成的标识，以保持给定的瞬时状态实例。|
|void saveOrUpdate(Object object)|保存（对象）或更新（对象）给定的实例。|
|void update(Object object)|更新带有标识符且是给定的处于脱管状态的实例的持久化实例。|
|void update(String entityName, Object object)|更新带有标识符且是给定的处于脱管状态的实例的持久化实例。|