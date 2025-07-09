# productos
codigo para leer productos usando record punteros array

{se desea gestionar una lista fija de hasta 10 productos en una tienda. Cada producto tiene:
Código (entero)
Precio (real)
Stock (entero)
Se debe usar un vector de punteros a productos.
Parte A – Cargar productos
Escribí un procedimiento cargarProductos que reciba el vector y una variable dimL (dimensión lógica),
y permita cargar hasta 10 productos, leyendo desde teclado. Usá new para reservar memoria para cada puntero.

📌 Parte B – Buscar producto por código
Escribí una función que reciba un código y devuelva el índice del producto en el vector (o 0 si no está). 
Si está, mostrará también el precio y stock del producto.
📌 Parte C – Modificar stock
Escribí un procedimiento que reciba un código y un valor entero. Si el producto existe, aumentá su stock
en ese valor. Si no existe, mostrará un mensaje.

📌 Parte D – Agregar producto
Escribí un procedimiento que permita agregar un producto nuevo solo si hay espacio (dimL < 10)
y si el código no se repite.

📌 Parte E – Informar todo
Imprimí todos los productos, mostrando: código, precio y stock.}

program punteros;
 const  
  dimf=10;
type 
  producto=record 
    codigo:integer;
    precio:real;
    stock:integer;
  end;
  vector=array[1..dimf] of ^producto ;
procedure cargarproductos(var v:vector;var diml:integer);
var
 seguir:string;
 i:integer;
 begin
  writeln('quiere cargar datos escriba la palabra :si ');
  readln(seguir);
  diml:=0;
  i:=1;
  while (diml<dimf) and (seguir='si') do  begin
   
   new(v[i]);
   writeln('ingrrese el codigo del producto');
   readln(v[i]^.codigo);
   writeln('ingrerse el precio del producto');
   readln(v[i]^.precio);
   writeln('ingrese el stock disponible');
   readln(v[i]^.stock);
   diml:=diml+1;
   i:=i+1;
   writeln('aun quiere seguir cargando datos si ese es el caso presione :si');
   readln(seguir);
  end;
 end;
 {📌 Parte B – Buscar producto por código
Escribí una función que reciba un código y devuelva el índice del producto en el vector (o 0 si no está). 
Si está, mostrará también el precio y stock del producto.}
function buscarproducto(v:vector;diml:integer ;codigo:integer):integer;
var
 seguir:boolean;
 i,pos:integer;
begin
  i:=1;
  seguir:=true;
  pos:=0;
  while (i<=diml) and (seguir)  do begin 
   if (v[i]^.codigo=codigo) then 
    begin
     writeln('el precio y el stock del producto con codigo:',codigo, 'es :precio ',v[i]^.precio:2:0,' stock disponible',v[i]^.stock);
     seguir:=false;
     pos:=i;
    end;
   i:=i+1;
  end;
  buscarproducto:=pos;
end;
{ Parte C – Modificar stock
Escribí un procedimiento que reciba un código y un valor entero. Si el producto existe, aumentá su stock
en ese valor. Si no existe, mostrará un mensaje.
}
procedure modificarstock(var v:vector;diml:integer;codigo:integer;valor:integer);
var
 seguir:boolean;
 i:integer;
begin
 seguir:=true;
 i:=1;
 while (i<=diml) and (seguir) do begin 
  if v[i]^.codigo=codigo then  begin
    v[i]^.stock:=v[i]^.stock + valor;
    seguir:=false;
   end;
   i:=i+1;
  end;
 if seguir=true then 
   writeln('no existe un producto con el codigo:',codigo);
end;
{📌 Parte D – Agregar producto
Escribí un procedimiento que permita agregar un producto nuevo solo si hay espacio (dimL < 10)
y si el código no se repite.}
procedure agregarproducto(var v:vector;var diml:integer);
var
 repetido:boolean;
 codigon,i:integer;
begin
   
 repetido:=false;
 if diml<dimf then begin
   writeln('ingrese el codigo del producto');
   readln(codigon);
   for i:=1 to diml do  
   begin 
     if codigon= v[i]^.codigo then begin
      repetido:= true;
      end;
   end;
   if repetido=false then begin
     diml:=diml+1;
     new(v[diml]);
     
     v[diml]^.codigo:=codigon;
     writeln('ingrese el precio del producto');
     readln(v[diml]^.precio);
     writeln('ingrese el stock disponible');
     readln(v[diml]^.stock);
   end
   else 
     writeln('el codigo es repetido');
 end;
end;
var 
  v:vector;
  dl:integer;
  codigo,valor,i:integer;
begin 
  cargarproductos(v,dl);
  writeln('ingrese el codigo del producto que desea buscar');
  readln(codigo);
  buscarproducto(v,dl,codigo);
  writeln('ingrese codigo  del producto que desea agregar ');
  readln(codigo);
  writeln('ingrese un valor ');
  readln(valor);
  modificarstock(v,dl,codigo,valor);
  agregarproducto(v,dl);
  for i:=1 to dl do begin 
   writeln('codigo: ',v[i]^.codigo);
   writeln('precio: ',v[i]^.precio:2:0);
   writeln('stock disponible: ',v[i]^.stock);
  end;
end.
