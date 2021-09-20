# Sample-Project


/* 
 * File: P3.c
 * Copy: Copyright (c) 2020 Elizabeth N. Romanos
 * BlazerID: eromanos
 * Vers: 2.0.1 9/20/2020 ENR - Did final touches 
 * Vers: 2.0.0 9/12/2020 ENR - Worked on it some
 * Vers: 1.0.0 9/08/2020 ENR - Original Coding
 * Desc: Utilizing functions build a command line utility that will 
 * calculate variable physics formulas.
 * Date Assigned: 09-08-2020 
 * Date Due: 12-11-2020

*/

#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <string.h>

#define a_y_init -32.2 

/* Function Prototype */
int help(void);
int projectile_1D_v2(double y_init);
int projectile_2D_v2(double v_init, double theta);
int simple_supported_beam_v2(double W, double L, double a);


int main(int argc, char** argv) {
    int i;
    int results;
    double y_init;
    double v_init;
    double theta;
    double W; // weight
    double L; // Beam length
    double a; // location on the beam
       
    // argc - number of arguments
    // argv - arguments themselves
    
    printf("Number of Arguments: %i\n", argc); // Number of input arguments
    printf("Value of first Arguments: %s\n", argv[0]); // zero (0) based index
    // starts with the number 0  
    // zeroth element of argv is the name of the executable
    // arguments 1...n are passed then to the executable
    // argv[1]
    // argv[2]
    
    printf("Value of all Arguments:\n");
    // Sample from Netbeans, modified - GCM
    for (i = 0; i < argc; i++) {
        printf("\t%i: %s\n", i, argv[i]);        
    }
    
            
    if (argc < 2) {
        // help implicitly called.
        help(); // print instructions to the user...
    } else {
       
        if (strcmp( argv[1], "/h" ) == 0) {
            // help explicitly called
            help();
        } 
        else if ((strcmp( argv[1], "/i" ) == 0 ) && (argc == 3)) 
        {
            printf("Interactive mode\n");
            
            if (( strcmp( argv[2], "/1D" ) == 0) ) {
                printf("Interactive/ 1D mode\n");
                // scanf to collect the y_init
                printf("Enter a height (ft):\n");
                scanf("%lf", &y_init);
                
                results = projectile_1D_v2( y_init );
                
            } else if ((strcmp( argv[2], "/2D") == 0) ) {
                printf("Interactive /2D mode\n");
                // scanf to collect v_init and theta
                printf("Enter in a v_init (ft/s):\n");
                scanf("%lf", &v_init);
                printf("Enter a theta (radians):\n");
                scanf("%lf", &theta);
                
                // we want to call the function...
                results = projectile_2D_v2( v_init, theta ); 
                //we would check to see if the results -- EXIT_SUCCESS
                
            }else if ((strcmp( argv[2], "/Beam") == 0)) {
                printf("Interactive /Beam mode\n");
                printf("Enter in W (lbs):\n");
                scanf("%lf", &W);
                printf("Enter in L (ft):\n");
                scanf("%lf", &L);
                printf("Enter in a (ft):\n");
                scanf("%lf", &a);
                
                results = simple_supported_beam_v2( W, L, a);
                
            }else {
                // implicitly ask for help
                printf("Unhandled mode\n");
                help();
            }
        } 
        else if (strcmp( argv[1], "/p" ) == 0) 
        {
            printf("Parameter mode\n");
            // identify if you have 3 or more arguments
            // scanf --> collected the initial height
            if (( strcmp( argv[2], "/1D") == 0) && ( argc == 4 )) 
            {
                // identify the third argument as /1D
                // /1D --> argc == 4
                // assume the fourth argument is the y_init
                y_init = strtod( argv[3], NULL );
                
                results = projectile_1D_v2( y_init );
            }
            else if ((strcmp( argv[2], "/2D") == 0) && (argc == 5 ))
            {
                // identify the third argument as /2D
                // /2D --> argc == 5
                // assume the fourth argument is the v_y_init 
                // assume the fifth argument is the angle in radians
                
                v_init = strtod( argv[3], NULL );
                theta = strtod( argv[4], NULL );
                
                // we want to call the function...
                results = projectile_2D_v2( v_init, theta );
                //we would check to see if the results -- EXIT_SUCCESS
                
            }    
            else if ((strcmp( argv[2], "/Beam") == 0) && (argc == 6))
            {
                // identify the third argument as /Beam
                // /Beam --> argc == 6
                // fourth --> load w
                // fifth --> length l
                // sixth --> placement a
                
                W = strtod( argv[3], NULL );
                L = strtod( argv[4], NULL );
                a = strtod( argv[5], NULL );
                
                // we want to call the function...
                results = simple_supported_beam_v2( W, L, a);
                
            }
            else 
            {
                // print out the help...  
                // implicit call for help
                help();
            }   
                        
        }         
        else 
        {
            // help implicitly called
            printf("Unhandled mode\n");
            help();            
        }
    }
        
    return (EXIT_SUCCESS);
}


/*
 * Name: int help(void)
 * Desc:  
 */
int help(void) {
    printf("========================================\n");
    printf("File: P3.exe\n");
    printf("Copy: Copyright (c) 2020 Elizabeth Romanos\n");
    printf("Vers: 1.0.0 09/08/2020 ENR - help function\n");
    printf("Desc: Physics Calculator\n");
    printf("========================================\n");
    printf("Usage:\n");
    printf("    /i - Interactive mode\n");
    printf("        /1D - One dimensional motion\n");
    printf("        /2D - Two dimensional motion\n");
    printf("        /Beam - Beam problem\n");
    printf("    /p - Parameter mode\n");
    printf("        /1D - One dimensional motion\n");
    printf("            requires initial height\n");
    printf("        /2D - Two dimensional motion\n");
    printf("            requires initial velocity and angle\n");
    printf("        /Beam - Beam problem\n");
    printf("    /h - Help\n");
    printf("========================================\n");
    printf("Examples:\n");
    printf("    /h\n"); // calls for help
    printf("    /i /1D\n");
    printf("    /i /2D\n"); 
    printf("    /i /Beam\n");
    printf("    /p /1D 100\n");    
    printf("    /p /2D 100 .7071\n");  
    printf("    /p /Beam 100 .7071 10\n"); 
    
    return (EXIT_SUCCESS);
}


/*
 * Name: int projectile_1D_v2(double y_init)
 * Desc: Calculates the amount of time taken from an object to drop from an 
 * initial height as well as the final velocity.
 * Args:
 *      double y_init - initial height
 */
int projectile_1D_v2(double y_init) {
    // we do not have to collect the value inside the function.
    // where we collect the value of y_init
    //        /i --> interactive scanf in main
    //        /p --> argv[?] where ? is the index of the argument vector
    // note: we probably should do some additional error checking
    //       Check to see if it is null (do this later)
    //       y_init must be positive 
    
    double y_final; 
    double v_y_init; 
    double v_y_final; 
    double t_init; 
    double t_final; 
    
    y_final = 0.0; // note: this does not have to be the case... 
    v_y_init = 0.0; 
    v_y_final = 0.0; 
    t_init = 0.0; 
    t_final = 0.0; 
    
    t_final = sqrt(( -2 * y_init ) / a_y_init ); 
    v_y_final = v_y_init + (a_y_init * t_final);
    
    printf("Description                       Value\n");
    printf("=========================================\n");
    // Input Values
    printf("y_init                            %.2f ft\n", y_init ); 
    printf("y_final                            %.2f ft\n", y_final ); 
    printf("t_init                             %.2f s\n", t_init ); 
    printf("v_y_init                           %.2f ft/s\n", v_y_init );
    printf("a_y_init                         %.2f ft/s^2\n", a_y_init );
    printf("=========================================\n");
    // Output Values
    printf("t_final                            %.2f s\n", t_final);
    printf("v_y_final                        %.2f ft/s\n", v_y_final);
    printf("=========================================\n");       
        
    
    
    
    
    return (EXIT_SUCCESS);        
}  


/* 
 * Name: int projectile_2D_v2(double v_init, double theta)
 * Desc: represents 2-dimensional motion
 * Args:
 *      double v_init - initial velocity
 *      double theta 
 */
int projectile_2D_v2(double v_init, double theta) {
    // similar to P2
    // do not declare v_init or the theta inside the function
    // get those values from main...
    //      /i - scanf in main
    //      /p - argv[?] and argv[? +1]
    
    
    double y_init; // initial height (ft)
    double y_final; // final height (ft)
    double x_init; // initial length (ft)
    double x_final; // final length (ft)
    double t_init; // initial time (sec)
    double t_final; // final time (sec)
    double v_y_init;
    double v_x_init; // initial velocity in the x direction (ft/s)
    double v_final; // final velocity (ft/s)
    double v_x_final; // final velocity in the x direction (ft/s)
    double v_y_final; // final velocity in the y direction (ft/s)
   
    // initialize or collect everything...
    y_init = 0.0 ; // assumed to be zero
    y_final = 0.0; // assumed to be zero
    x_init = 0.0; // assumed to be zero
    x_final = 0.0; // will calculate later... - Output
    t_init = 0.0; // the clock starts...
    t_final = 0.0; // will calculate later... - Output
    v_y_init = 0.0;
    v_x_init = 0.0; // will calculate later - Output
    v_final = 0.0; // will calculate later
    v_x_final = 0.0; // will calculate later
    v_y_final = 0.0; // will calculate later - Output
   
    
    // Calculate initial velocity in the x direction v_x_init
    v_x_init = ((v_init)*cos(theta) );  
    
    // Calculate initial velocity in the y direction v_y_init
    v_y_init = ( (v_init) * sin(theta) );  
    
    // Calculate the final length of time t_final
    t_final = ( (-2 * (v_y_init) ) / (a_y_init) ); 
    
    // Calculate the final position in the x direction  x_final
    x_final = ( (x_init) + ( (v_x_init) * (t_final) ) + ( 0.5*( (a_y_init) * (pow( (t_final), 2) ) ) ) ); 
    
    // Calculate the final velocity in the x direction  v_x_final
    v_x_final = ( (v_x_init) + ( (a_y_init) * (t_final) ) ); 
    
    // Calculate the final velocity in the y direction v_y_final
    v_y_final = ( (v_y_init) + ( (a_y_init) * (t_final) ) ); 
    
    // Calculate the final overall velocity v_final
    v_final = sqrt( (pow( (v_init), 2) ) + (2*( (a_y_init) * (x_final) ) ) );
    
    
    // Print a nice table...
    printf("Description                       Value\n");
    printf("=========================================\n");
    // Input Values
    printf("y_init                            %.2f ft\n", y_init);
    printf("y_final                           %.2f ft\n", y_final);
    printf("x_init                            %.2f ft\n", x_init);
    printf("t_init                            %.2f s\n", t_init);
    printf("v_init                            %.2f ft/s\n", v_init);
    printf("v_final                          %.2f ft/s\n", v_final);
    printf("v_x_final                         %.2f ft/s\n", v_x_final);
    printf("theta                             %.2f radians\n", theta);
    printf("a_y_init                        %.2f ft/s^2\n", a_y_init);
    printf("=========================================\n");
    // Output Values
    printf("v_x_init                         %.2f ft/s\n", v_x_init); 
    printf("v_y_init                         %.2f ft/s\n", v_y_init); 
    printf("t_final                           %.2f s\n", t_final);
    printf("x_final                         %.2f ft\n", x_final); 
    printf("v_y_final                       %.2f ft/s\n", v_y_final);
    printf("=========================================\n");
    
    return (EXIT_SUCCESS);
}



/* 
 * Name: int simple_supported_beam_v2(double W, double L, double a)
 * Desc: represents a simple supported beam
 * Args:
 *      double W - weight
 *      double L - length
 *      double a - location of the beam
 *  
 */
int simple_supported_beam_v2(double W, double L, double a){
    
    double R1; // reaction at P1
    double R2; // reaction at P2
    
    //initialize or collect everything...
    R1 = 0.0; // calculate later
    R2 = 0.0; // calculate later
    
     // Calculate the reaction at P2 - R2
    R2 = ( (W * a) / L );
    
    // Calculate the reaction at P1 - R1
    R1 = ( ( W - R2) ); 
    
    // Print a nice table...
    printf("Description                       Value\n");
    printf("=======================================\n");
    // Input Values
    printf("W                                 %.2f lbs\n", W); 
    printf("L                                 %.2f ft\n", L); 
    printf("a                                 %.2f ft\n", a); 
    printf("=======================================\n");
    // Output Values
    printf("R1                                %.2f lbs\n", R1); 
    printf("R2                                %.2f lbs\n", R2); 
    printf("=======================================\n");
    
    
   return (EXIT_SUCCESS);
}
