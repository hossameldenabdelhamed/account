alter proc Balance
@par1 nvarchar(50)
as
declare @MCRe int
declare @MDi int
begin
set @MCRe=(select sum(credit) from day2 where account_guid=@par1)
set @MDi=(select sum(debit) from day2 where account_guid=@par1)
if(@MCRe>@MDi)
begin 
print 'Balance= debit' 
(select sum(credit) - sum(debit) from day2 where account_guid=@par1)  
end 
else
begin 
print 'balance= credit' 
(select sum(debit) - sum(credit) from day2 where account_guid=@par1)  
end
end
--------------------------------------------------------------

exec Balance '25878987-5478-6547-5897-254789654123'
--------------------------------------------
