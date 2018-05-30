# Molecular-Dynamic
This code can be used for the study of classical gases with weak interaction (Van der Waals). The evolution of the system is done by the ```Speed Verlet algorithm```.
#### Pipe in gnuplot

In ```linux``` you can call ```gnuplot``` from your ```c``` code as follows:

```c
FILE *pipe = popen("gnuplot", "w");
assert(pipe);
/*
Development code of our program
*/
pclose(pipe);
```
This form of call can be used in a ```window```, provided that the compilation of the code is done through a console (```gnuplot``` and ```gcc```) must be environment variables.

```c
/*
Impresión que permite visualizar la evolución del sistema.
Keyword Arguments:
sys: class_system * (sistema de particulas).
gnuplot_pipe: ----> variable de entorno (Window).
              ----> objeto FILE * (Linux).
*/
void printer_system(class_system *sys, FILE *gnuplot_pipe){
    int i;
   
    fprintf(gnuplot_pipe, "set title '{/=20 Modelo de Gas, pass %d}'\n", sys->accountant);
    fprintf(gnuplot_pipe, "set xlabel  '{/=15 X}'\n");  
    fprintf(gnuplot_pipe, "set zlabel  '{/=15 Z}'\n");
    fprintf(gnuplot_pipe, "set ylabel  '{/=15 Y}'\n");
    fprintf(gnuplot_pipe, "splot '-' with p pointtype 6 t ''\n");
  
    for(i = 0; i < N; i++)
        fprintf(gnuplot_pipe, "%lf\t%lf\t%lf\n", sys -> position[i][0], 
                                    sys -> position[i][1], sys ->position[i][2]);
    
    fprintf(gnuplot_pipe, "e\n");
    fflush(gnuplot_pipe);
}
```
