# utl-changepoint-like-analysis-in-R-and-SAS-elbow-graph
Changepoint like analysis in R and SAS elbow graph 
    Changepoint like analysis in R and SAS elbow graph                                                                                
                                                                                                                                      
     Optimum hingepoint for a horizontal and sloping line                                                                             
                                                                                                                                      
      Two Solutions                                                                                                                   
                                                                                                                                      
          a. SAS nlmixed                                                                                                              
          b. R package changepoint                                                                                                    
          c. Python knee locator (locates the best existing )x,y) for the honge point)                                                
             https://github.com/arvkevi/kneed                                                                                         
             Once you have the hingepoint you can fit translate two lines                                                             
             and fit two 0 intercept models                                                                                           
                                                                                                                                      
    Related two but slightly simpler                                                                                                  
    SAS Forum                                                                                                                         
    https://tinyurl.com/yxf8wwfv                                                                                                      
    https://communities.sas.com/t5/SAS-Studio/How-to-Perform-Change-Point-Analysis/m-p/592448                                         
                                                                                                                                      
    github                                                                                                                            
    https://tinyurl.com/y5jtpwtq                                                                                                      
    https://stats.stackexchange.com/questions/291436/anchoring-a-linear-regression-to-a-specific-data-point-in-r/291672#291672        
                                                                                                                                      
    *_                   _                                                                                                            
    (_)_ __  _ __  _   _| |_                                                                                                          
    | | '_ \| '_ \| | | | __|                                                                                                         
    | | | | | |_) | |_| | |_                                                                                                          
    |_|_| |_| .__/ \__,_|\__|                                                                                                         
            |_|                                                                                                                       
    ;                                                                                                                                 
                                                                                                                                      
    options validvarname=upcase;                                                                                                      
    libname sd1 "d:/sd1";                                                                                                             
    data sd1.have;                                                                                                                    
    INPUT id $ x y;                                                                                                                   
    cards4;                                                                                                                           
    1   1  0.22                                                                                                                       
    2   2  0.22                                                                                                                       
    3   3  0.32                                                                                                                       
    4   4  0.51                                                                                                                       
    5   5  0.58                                                                                                                       
    6   6  1.10                                                                                                                       
    7   7  1.60                                                                                                                       
    8   8  2.85                                                                                                                       
    9   9  3.45                                                                                                                       
    ;;;;                                                                                                                              
    run;quit;                                                                                                                         
                                                                                                                                      
                                                                                                                                      
    SD1.HAVE total obs=9                                                                                                              
                                                                                                                                      
      ID    X      Y                                                                                                                  
                                                                                                                                      
      1     1    0.22                                                                                                                 
      2     2    0.22                                                                                                                 
      3     3    0.32                                                                                                                 
      4     4    0.51                                                                                                                 
      5     5    0.58                                                                                                                 
      6     6    1.10                                                                                                                 
      7     7    1.60                                                                                                                 
      8     8    2.85                                                                                                                 
      9     9    3.45                                                                                                                 
                                                                                                                                      
    options ls=64 ps=44;                                                                                                              
    %let y=y123456789012345678901234567890;                                                                                           
    proc plot data=sd1.have(rename=y=&y);                                                                                             
    plot &y*x='*' / box;;                                                                                                             
    run;quit;                                                                                                                         
                                                                                                                                      
           1  2  3  4  5  6  7  8  9                                                                                                  
        ---+--+--+--+--+--+--+--+--+---                                                                                               
        |          MODEL              |                                                                                               
        |                             |                                                                                               
      4 +(x<=T)*B0+(x>T)*(B0+B1*(x-T))+ 4                                                                                             
        |                             |                                                                                               
        | CONSTANT FOR X<=T           |                                                                                               
        | T is changepoint         *  |                                                                                               
        |                             |                                                                                               
        |                             |                                                                                               
      3 +                             + 3                                                                                             
        |                       *     |                                                                                               
        |                             |                                                                                               
        |                             |                                                                                               
        |                             |                                                                                               
        |                             |                                                                                               
      2 +                             + 2                                                                                             
        |                             |                                                                                               
        |                    *        |                                                                                               
        |                             |                                                                                               
        |                             |                                                                                               
        |                 *           |                                                                                               
      1 +                             + 1                                                                                             
        |                             |                                                                                               
        |                             |                                                                                               
        |           *  *              |                                                                                               
        |        *                    |                                                                                               
        |  *  *                       |                                                                                               
      0 +                             + 0                                                                                             
        |                             |                                                                                               
        ---+--+--+--+--+--+--+--+--+---                                                                                               
           1  2  3  4  5  6  7  8  9                                                                                                  
                                                                                                                                      
                       X                                                                                                              
                         X                                                                                                            
    *            _               _                                                                                                    
      ___  _   _| |_ _ __  _   _| |_                                                                                                  
     / _ \| | | | __| '_ \| | | | __|                                                                                                 
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                  
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                 
                    |_|                                                                                                               
      __ _      ___  __ _ ___                                                                                                         
     / _` |    / __|/ _` / __|                                                                                                        
    | (_| |_   \__ \ (_| \__ \                                                                                                        
     \__,_(_)  |___/\__,_|___/                                                                                                        
                                                                                                                                      
    ;                                                                                                                                 
                        X                                                                                                             
          0        3        6        9                                                                                                
       ---+--------+--------+--------+----                                                                                            
       |             MODELS              |                                                                                            
       |             ======              |                                                                                            
     4 + (x<=5)*B0+(x>t0)*(B0+B1*(x-T0)) + 4                                                                                          
       |                                 |                                                                                            
       |  P - Predicted                  |                                                                                            
       |  * - Observed               *   |                                                                                            
       |                             P   |                                                                                            
       |  B0 = 0.37    T0=5.23           |                                                                                            
     3 +  B1 = 0.83        ^             + 3                                                                                          
       |  T0 = 5.23        |      *      |                                                                                            
       |                   |      P      |                                                                                            
    Y  |                   |             |                                                                                            
       |                   |             |                                                                                            
       |                   |             |                                                                                            
     2 +                   |             + 2                                                                                          
       |                   |   P         |                                                                                            
       |                   |    *        |                                                                                            
       |                   |             |                                                                                            
       |                   |             |                                                                                            
       |                   | *           |                                                                                            
     1 +       MODEL       |P            + 1                                                                                          
       |       Y=.37       | Y=-4+.83 x  |                                                                                            
       |                   |             |                                                                                            
       |              *  * |             |                                                                                            
       |     P  P  *  P  P |             |                                                                                            
       |     *  *          |             |                                                                                            
     0 +                   |             + 0                                                                                          
       |                  5.23           |                                                                                            
       ---+--------+--------+--------+----                                                                                            
          0        3        6        9                                                                                                
                       X                                                                                                              
                                                                                                                                      
    Up to 40 obs from PARMS total obs=4                                                                                               
                                                                                                                                      
    Obs    PARAMETER    ESTIMATE                                                                                                      
                                                                                                                                      
     1      B0           0.37                                                                                                         
     2      B1           0.83                                                                                                         
     3      t0           5.23                                                                                                         
                                                                                                                                      
                                                                                                                                      
    WANT total obs=10                                                                                                                 
                                                                                                                                      
       X       Y      EST      DIF                                                                                                    
                                                                                                                                      
      1.00    0.22    0.37    -0.15                                                                                                   
      2.00    0.22    0.37    -0.15                                                                                                   
      3.00    0.32    0.37    -0.05                                                                                                   
      4.00    0.51    0.37     0.14                                                                                                   
      5.00    0.58    0.37     0.21                                                                                                   
      6.00    1.10    1.00     0.10                                                                                                   
      7.00    1.60    1.83    -0.23                                                                                                   
      8.00    2.85    2.67     0.18                                                                                                   
      9.00    3.45    3.50    -0.05                                                                                                   
                             ========                                                                                                 
                              sum=0                                                                                                   
    *_                                                                                                                                
    | |__      _ __                                                                                                                   
    | '_ \    | '__|                                                                                                                  
    | |_) |   | |                                                                                                                     
    |_.__(_)  |_|                                                                                                                     
                                                                                                                                      
    ;                                                                                                                                 
                                                                                                                                      
                                                                                                                                      
    WORK.COEF total obs=3                                                                                                             
                                                                                                                                      
       DES       COEF                                                                                                                 
                                                                                                                                      
       a       -3.97                                                                                                                  
       b        0.83                                                                                                                  
       r        5.23                                                                                                                  
                                                                                                                                      
    WORK.WANT total obs=9                                                                                                             
                            R      SAS                                                                                                
     X      Y     EST      DIF      R                                                                                                 
                                                                                                                                      
     1    0.22    0.37    -0.15   -0.15                                                                                               
     2    0.22    0.37    -0.15   -0.15                                                                                               
     3    0.32    0.37    -0.05   -0.05                                                                                               
     4    0.51    0.37     0.14    0.14                                                                                               
     5    0.58    0.37     0.21    0.21                                                                                               
     6    1.10    1.01     0.09    0.10                                                                                               
     7    1.60    1.84    -0.24   -0.23                                                                                               
     8    2.85    2.66     0.19    0.18                                                                                               
     9    3.45    3.49    -0.04   -0.05                                                                                               
                                                                                                                                      
                        X                                                                                                             
          0        3        6        9                                                                                                
       ---+--------+--------+--------+----                                                                                            
       |             MODELS              |                                                                                            
       |             ======              |                                                                                            
     4 + (x<=5)*B0+(x>t0)*(B0+B1*(x-T0)) + 4                                                                                          
       |                                 |                                                                                            
       |  P - Predicted                  |                                                                                            
       |  * - Observed               *   |                                                                                            
       |                             P   |                                                                                            
       |  B0 = 0.37    T0=5.23           |                                                                                            
     3 +  B1 = 0.83        ^             + 3                                                                                          
       |  T0 = 5.23        |      *      |                                                                                            
       |                   |      P      |                                                                                            
    Y  |                   |             |                                                                                            
       |                   |             |                                                                                            
       |                   |             |                                                                                            
     2 +                   |             + 2                                                                                          
       |                   |   P         |                                                                                            
       |                   |    *        |                                                                                            
       |                   |             |                                                                                            
       |                   |             |                                                                                            
       |                   | *           |                                                                                            
     1 +       MODEL       |P            + 1                                                                                          
       |       Y=.37       | Y=-4+.83 x  |                                                                                            
       |                   |             |                                                                                            
       |              *  * |             |                                                                                            
       |     P  P  *  P  P |             |                                                                                            
       |     *  *          |             |                                                                                            
     0 +                   |             + 0                                                                                          
       |                  5.23           |                                                                                            
       ---+--------+--------+--------+----                                                                                            
          0        3        6        9                                                                                                
                       X                                                                                                              
    *                        _                                                                                                        
      ___      _ __  _   _  | | ___ __   ___  ___                                                                                     
     / __|    | '_ \| | | | | |/ / '_ \ / _ \/ _ \                                                                                    
    | (__ _   | |_) | |_| | |   <| | | |  __/  __/                                                                                    
     \___(_)  | .__/ \__, | |_|\_\_| |_|\___|\___|                                                                                    
              |_|    |___/                                                                                                            
    ;                                                                                                                                 
                                                                                                                                      
    X value of hinge point 5.0                                                                                                        
                                                                                                                                      
                                                                                                                                      
                                                                                                                                      
    *                                                                                                                                 
     _ __  _ __ ___   ___ ___  ___ ___                                                                                                
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                               
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                               
    | .__/|_|  \___/ \___\___||___/___/                                                                                               
    |_|                                                                                                                               
      __ _      ___  __ _ ___                                                                                                         
     / _` |    / __|/ _` / __|                                                                                                        
    | (_| |_   \__ \ (_| \__ \                                                                                                        
     \__,_(_)  |___/\__,_|___/                                                                                                        
                                                                                                                                      
    ;                                                                                                                                 
                                                                                                                                      
    ods trace on;                                                                                                                     
    ods output parameterestimates=parms(keep=parameter estimate);                                                                     
    proc nlmixed data=sd1.have;                                                                                                       
        parms B0 = 0 B1=1 t0=5 sigma_r=1;                                                                                             
        mu1 = (x <= t0)*B0;                                                                                                           
        mu2 = (x > t0)*(B0 + B1*(x - t0));                                                                                            
        mu=mu1+mu2;                                                                                                                   
        model y~normal(mu,sigma_r);                                                                                                   
    run;                                                                                                                              
    ods trace off;                                                                                                                    
                                                                                                                                      
    data want(KEEP=X Y EST DIF);                                                                                                      
      set parms(where=(parameter="B0")); B0=estimate;                                                                                 
      set parms(where=(parameter="B1")); B1=estimate;                                                                                 
      set parms(where=(parameter="t0")); T0=estimate;                                                                                 
      do until (dne);                                                                                                                 
        set sd1.have end=dne;                                                                                                         
        format x y est dif 5.2;                                                                                                       
        est =  (x <= 5)*B0 + (x > t0 )*(B0 + B1*(x-T0));                                                                              
        dif = y-est;                                                                                                                  
        output;                                                                                                                       
      end;                                                                                                                            
    run;quit;                                                                                                                         
                                                                                                                                      
    options ls=72 ps=44;                                                                                                              
    %let y=y123456789012345678901234567890;                                                                                           
    proc plot data=want(rename=y=&y);                                                                                                 
    plot &y*x='*' est*x="P" / overlay box;                                                                                            
    run;quit;                                                                                                                         
                                                                                                                                      
    *_                                                                                                                                
    | |__      _ __                                                                                                                   
    | '_ \    | '__|                                                                                                                  
    | |_) |   | |                                                                                                                     
    |_.__(_)  |_|                                                                                                                     
                                                                                                                                      
    ;                                                                                                                                 
                                                                                                                                      
    %utlfkil(d:/xpt/want.xpt);                                                                                                        
                                                                                                                                      
    %utl_submit_r64('                                                                                                                 
    library(haven);                                                                                                                   
    library(SASxport);                                                                                                                
    fitDat<-read_sas("d:/sd1/have.sas7bdat")[,2:3];                                                                                   
    fitDat;                                                                                                                           
    a.ini     =   .3;                                                                                                                 
    b.ini     =    1;                                                                                                                 
    clx.ini   =    5;                                                                                                                 
                                                                                                                                      
    platlin = function(x, a, b, clx)                                                                                                  
              {ifelse(x < clx, a + b * clx,                                                                                           
                               a + b * x)};                                                                                           
                                                                                                                                      
    model = nls(Y ~ platlin(X, a, b, clx),                                                                                            
                data = fitDat,                                                                                                        
                start = list(a   = a.ini,                                                                                             
                             b   = b.ini,                                                                                             
                             clx = clx.ini),                                                                                          
                 trace = FALSE,                                                                                                       
                 nls.control(tol=.001));                                                                                              
    coef<-summary(model)$coefficients[,1:3][,1];                                                                                      
    coef<-as.data.frame(coef);                                                                                                        
    coef$DES<-rownames(coef);                                                                                                         
    coef;                                                                                                                             
    i=(1:9);                                                                                                                          
    D1 = data.frame(X = i);                                                                                                           
    want = as.data.frame(predict(model, D1));                                                                                         
    colnames(want)<-"EST";                                                                                                            
    want;                                                                                                                             
    write.xport(want,coef,file="d:/xpt/want.xpt");                                                                                    
    ');                                                                                                                               
                                                                                                                                      
                                                                                                                                      
    libname xpt xport "d:/xpt/want.xpt";                                                                                              
                                                                                                                                      
    data want;                                                                                                                        
      set xpt.want;                                                                                                                   
    run;quit;                                                                                                                         
                                                                                                                                      
    data coef;                                                                                                                        
      set xpt.coef;                                                                                                                   
    run;quit;                                                                                                                         
                                                                                                                                      
    libname xpt clear;                                                                                                                
                                                                                                                                      
    data want (KEEP=X Y EST DIF);                                                                                                     
      set coef(where=(des="a"));   a   =coef;                                                                                         
      set coef(where=(des="b"));   b   =coef;                                                                                         
      set coef(where=(des="clx")); clx =coef;                                                                                         
      do until (dne);                                                                                                                 
        set sd1.have end=dne;                                                                                                         
        format x y est dif 5.2;                                                                                                       
        format x y est dif 5.2;                                                                                                       
        est =  (x <= clx)*(a + b * clx) + (x > clx )*(a + b * x);                                                                     
        dif = y-est;                                                                                                                  
        output;                                                                                                                       
      end;                                                                                                                            
    run;quit;                                                                                                                         
                                                                                                                                      
    options ls=72 ps=44;                                                                                                              
    %let y=y123456789012345678901234567890;                                                                                           
    proc plot data=want(rename=y=&y);                                                                                                 
    plot &y*x='*' est*x="P" / overlay box;                                                                                            
    run;quit;                                                                                                                         
                                                                                                                                      
    *                        _                        _                                                                               
      ___      _ __  _   _  | | ___ __   ___  ___  __| |                                                                              
     / __|    | '_ \| | | | | |/ / '_ \ / _ \/ _ \/ _` |                                                                              
    | (__ _   | |_) | |_| | |   <| | | |  __/  __/ (_| |                                                                              
     \___(_)  | .__/ \__, | |_|\_\_| |_|\___|\___|\__,_|                                                                              
              |_|    |___/                                                                                                            
    ;                                                                                                                                 
                                                                                                                                      
    %symdel frompy  nowarn;                                                                                                           
                                                                                                                                      
    %utl_submit_py64_37('                                                                                                             
    import pandas as pd;                                                                                                              
    import numpy as np;                                                                                                               
    import pyperclip;                                                                                                                 
    from kneed import DataGenerator, KneeLocator;                                                                                     
    import pyreadstat;                                                                                                                
    want, meta = pyreadstat.read_sas7bdat("d:/sd1/hav.sas7bdat");                                                                     
    print(want);                                                                                                                      
    X=want.ix[:,0];                                                                                                                   
    Y=want.ix[:,1];                                                                                                                   
    kneedle = KneeLocator(want.ix[:,0], want.ix[:,1], S=1.0, curve="convex", direction="increasing");                                 
    print(round(kneedle.knee, 8));                                                                                                    
    ot=str(round(kneedle.knee, 8));                                                                                                   
    pyperclip.copy(ot);                                                                                                               
    ',return=frompy);                                                                                                                 
                                                                                                                                      
    %put X value of hinge point &frompy;                                                                                              
                                                                                                                                      
                                                                                                                                      
