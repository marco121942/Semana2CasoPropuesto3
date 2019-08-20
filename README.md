# Semana2CasoPropuesto3
create procedure usp_nombre_meses @anio int
as
select distinct MONTH(FechaPedido) as 'idMeses', DateName(month,FechaPedido) as meses from Pedidos
where YEAR(FechaPedido) = @anio;


create procedure usp_filtrar_pedidos_año_mes
@anio varchar(4),
@mes varchar(2)
as
select IdPedido,FechaPedido,FechaEntrega,DATEDIFF(year,FechaEntrega,GETDATE()) as 'Transcurridos',Empleados.Nombre from Pedidos
inner join Empleados on Empleados.IdEmpleado = Pedidos.IdEmpleado
where FechaPedido BETWEEN @anio+'-'+@mes+'-01' AND  @anio+'-'+@mes+'-31'
