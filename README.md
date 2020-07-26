/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package tableroajedrez;



/**
 *
 * @author USUARIO
 */
public class resolverejercicio {
    private    int posicionocupadaenTablerox[]=new int [64]; //ubicacion del caballo en y segun el numero de iteracion
    private    int posicionocupadaenTableroy[]=new int [64]; //ubicacion del caballo en x segun el numero de iteracion
    private final   boolean posicionocupada[][]=new boolean [8][8]; //almacena las casillas ya ocupadas
    private final int pesoPosicionesTablero[][]={{2,3,4,4,4,4,3,2}, //describimos los pesos de cada casilla en el tablero
                                                 {3,4,6,6,6,6,4,3},
                                                 {4,6,8,8,8,8,6,4},
                                                 {4,6,8,8,8,8,6,4},
                                                 {4,6,8,8,8,8,6,4},
                                                 {4,6,8,8,8,8,6,4},
                                                 {3,4,6,6,6,6,4,3},
                                                 {2,3,4,4,4,4,3,2}}; 
    private  final  int movimientoCaballohorizontal[]=new int [8];
    private  final int movimientoCaballovertical[]=new int [8];
    private int mejorOpcion=0;
    
    public resolverejercicio(int x[],int y[],int iniciox, int inicioy)
    {
    posicionocupadaenTablerox=x;
    posicionocupadaenTableroy=y;
    posicionocupadaenTablerox[0]=iniciox;
    posicionocupadaenTableroy[0]=inicioy;
    posicionocupada[iniciox][inicioy]=true;
  
    
    }
    
    public boolean relizarSaltos()
    {
     boolean solucion=false;
     movimientoCaballohorizontal[0]=2;movimientoCaballovertical[0]=-1;
     movimientoCaballohorizontal[1]=1;movimientoCaballovertical[1]=-2;
     movimientoCaballohorizontal[2]=-1;movimientoCaballovertical[2]=-2;
     movimientoCaballohorizontal[3]=-2;movimientoCaballovertical[3]=-1;
     movimientoCaballohorizontal[4]=-2;movimientoCaballovertical[4]=1;
     movimientoCaballohorizontal[5]=-1;movimientoCaballovertical[5]=2;
     movimientoCaballohorizontal[6]=1;movimientoCaballovertical[6]=2;
     movimientoCaballohorizontal[7]=2;movimientoCaballovertical[7]=1;
     int contador=64;

     int salto=0;
                for(int i=1;i<contador;i++)
                {
                    salto=opcionesSiguienteSaltoVacio(i);  
                    posicionocupadaenTablerox[i]=posicionocupadaenTablerox[i-1]+movimientoCaballohorizontal[salto];
                    posicionocupadaenTableroy[i]=posicionocupadaenTableroy[i-1]+movimientoCaballovertical[salto];
                    System.out.printf("%d: %d %d\n",i,posicionocupadaenTablerox[i],posicionocupadaenTableroy[i]); 
                    posicionocupada[posicionocupadaenTablerox[i]][posicionocupadaenTableroy[i]]=true;
                      
                }
             
            
       return true;
    }
    
        public boolean verificarPosicionesAnteriores(int i,int salto)
    {
   
    boolean ocupado=false;
    int sumax=posicionocupadaenTablerox[i-1]+movimientoCaballohorizontal[salto];
    int sumay=posicionocupadaenTableroy[i-1]+movimientoCaballovertical[salto];
            if(sumax>=0&&sumax<8 && sumay>=0&&sumay<8)
            {
                if(posicionocupada[sumax][sumay]==false) 
                {
//                    posicionocupada[sumax][sumay]=true;              
                    ocupado=true;
                }
            }           
    return ocupado;
        
    }
        
    public int opcionesSiguienteSaltoVacio(int i)
    {
     int contadoratorado=0;
     int salto=0;
     int mejoropcionprueba;
     boolean acumulaOpcionesNoOcupadas[]=new boolean[8];
     do{
           salto=contadoratorado;
           contadoratorado++;       
           if(verificarPosicionesAnteriores(i, salto)==true)
           {
               acumulaOpcionesNoOcupadas[salto]=true;
               mejorOpcion=salto;
           }
        }while(contadoratorado<8); 
        mejorOpcion=compararPesosTablero(i, acumulaOpcionesNoOcupadas);
//        }while(verificarPosicionesAnteriores(i, salto)==false);   
     return mejorOpcion;
    }
    
    
    public int compararPesosTablero(int i,boolean []opcionesNoOcupadas)
    {
        int mejoropcionx=0;
        int mejoropciony=0;
        int pesaje=0,pesajeA=9;
        int mejorP=0;
        for(int b=0;b<8;b++)
        {
            if(opcionesNoOcupadas[b]==true)
            {
                mejoropcionx=posicionocupadaenTablerox[i-1]+movimientoCaballohorizontal[b];
                mejoropciony=posicionocupadaenTableroy[i-1]+movimientoCaballovertical[b];
                pesaje=pesoPosicionesTablero[mejoropcionx][mejoropciony];
                if (pesajeA>pesaje)
                {
                    pesajeA=pesaje;
                    mejorP=b;
                }
            }
        }
    return mejorP;
    }
        
        
}
