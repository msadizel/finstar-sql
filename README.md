Использован синтаксис MS SQL

Задание 2.

select clientName, count(cc.id) as contactCount from clients c
left join clientContacts cc on c.id = cc.clientId
group by clientname

select c.* from clients c
left join clientContacts cc on c.id = cc.clientId
group by c.clientname, c.id
having count(cc.id) >= 2


Задание 3.

declare @dates table
(
    id bigint,
    dt date
)

insert into @dates (id,dt)
VALUES(1,'01.01.2021'), (1,'10.01.2021'), (1,'30.01.2021'), (2,'15.01.2021'), (2,'30.01.2021')

select *
from
    (
select id, dt as sd, ( select min(dt)
        from @dates d2
        where d2.id = d.id and d2.dt > d.dt) as ed
    from @dates d
) res
where ed is not null
