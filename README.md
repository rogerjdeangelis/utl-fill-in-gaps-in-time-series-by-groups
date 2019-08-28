# utl-fill-in-gaps-in-time-series-by-groups
Fill in gaps in time series by group
    Fill in gaps in time series by groups                                                                          
                                                                                                                   
    R has many timeseries functions.                                                                               
    Filling gaps is the first step.                                                                                
                                                                                                                   
    github                                                                                                         
    https://tinyurl.com/y427thnj                                                                                   
    https://github.com/rogerjdeangelis/utl-fill-in-gaps-in-time-series-by-groups                                   
                                                                                                                   
    Related to                                                                                                     
    SAS forum                                                                                                      
    https://tinyurl.com/y5y8awdw                                                                                   
    https://communities.sas.com/t5/SAS-Programming/Fill-in-a-date-table-from-a-specific-date/m-p/584534            
                                                                                                                   
    Draucut                                                                                                        
    https://communities.sas.com/t5/user/viewprofilepage/user-id/31304                                              
                                                                                                                   
    options validvarname=upcase;                                                                                   
    libname sd1 "d:/sd1";                                                                                          
    data sd1.have;                                                                                                 
      input name $ date :anydtdte7. value;                                                                         
    format date yymmdd10.;                                                                                         
    datalines;                                                                                                     
    NAME1 12/2017 2                                                                                                
    NAME1 03/2018 1                                                                                                
    NAME1 06/2018 3                                                                                                
    NAME2 01/2018 3                                                                                                
    NAME2 05/2018 4                                                                                                
    NAME2 07/2018 1                                                                                                
    ;;;;                                                                                                           
    run;quit;                                                                                                      
                                                                                                                   
    SD1.HAVE total obs=6                                                                                           
                                                                                                                   
      NAME      DATE      VALUE                                                                                    
                                                                                                                   
      NAME1    12/2017      2                                                                                      
      NAME1    03/2018      1                                                                                      
      NAME1    06/2018      3                                                                                      
                                                                                                                   
      NAME2    01/2018      3                                                                                      
      NAME2    05/2018      4                                                                                      
      NAME2    07/2018      1                                                                                      
                                                                                                                   
    *           _                                                                                                  
     _ __ _   _| | ___  ___                                                                                        
    | '__| | | | |/ _ \/ __|                                                                                       
    | |  | |_| | |  __/\__ \                                                                                       
    |_|   \__,_|_|\___||___/                                                                                       
                                                                                                                   
    ;                                    RULES                                                                     
      NAME      DATE      VALUE |   DATE      VALUE                                                                
                                |                                                                                  
      NAME1    12/2017      2   |   12/2017      2                                                                 
                                |                                                                                  
                                |   01/2018      0  Add these                                                      
                                |   02/2018      0                                                                 
                                |                                                                                  
      NAME1    07/2018      1   |   03/2018      1                                                                 
                                |                                                                                  
                                |   04/2018      0                                                                 
                                |   05/2018      0                                                                 
                                |                                                                                  
      NAME1    02/2019      3   |   06/2018      3                                                                 
                                                                                                                   
    *            _               _                                                                                 
      ___  _   _| |_ _ __  _   _| |_                                                                               
     / _ \| | | | __| '_ \| | | | __|                                                                              
    | (_) | |_| | |_| |_) | |_| | |_                                                                               
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                              
                    |_|                                                                                            
    ;                                                                                                              
                                                                                                                   
     WORK.WANT total obs=14                                                                                        
                                                                                                                   
      NAME      DATE      VALUE                                                                                    
                                                                                                                   
      NAME1    12/2017      2                                                                                      
      NAME1    01/2018      0                                                                                      
      NAME1    02/2018      0                                                                                      
      NAME1    03/2018      1                                                                                      
      NAME1    04/2018      0                                                                                      
      NAME1    05/2018      0                                                                                      
      NAME1    06/2018      3                                                                                      
                                                                                                                   
      NAME2    01/2018      3                                                                                      
      NAME2    02/2018      0                                                                                      
      NAME2    03/2018      0                                                                                      
      NAME2    04/2018      0                                                                                      
      NAME2    05/2018      4                                                                                      
      NAME2    06/2018      0                                                                                      
      NAME2    07/2018      1                                                                                      
                                                                                                                   
    *          _       _   _                                                                                       
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                       
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                                      
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                      
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                      
                                                                                                                   
    ;                                                                                                              
                                                                                                                   
    *____                                                                                                          
    |  _ \                                                                                                         
    | |_) |                                                                                                        
    |  _ <                                                                                                         
    |_| \_\                                                                                                        
                                                                                                                   
    ;                                                                                                              
                                                                                                                   
    options validvarname=upcase;                                                                                   
    libname sd1 "d:/sd1";                                                                                          
    data sd1.have;                                                                                                 
      input name $ date :anydtdte7. value;                                                                         
    format date yymmdd10.;                                                                                         
    datalines;                                                                                                     
    NAME1 12/2017 2                                                                                                
    NAME1 03/2018 1                                                                                                
    NAME1 06/2018 3                                                                                                
    NAME2 01/2018 3                                                                                                
    NAME2 05/2018 4                                                                                                
    NAME2 07/2018 1                                                                                                
    ;;;;                                                                                                           
    run;quit;                                                                                                      
                                                                                                                   
    %utl_submit_r64('                                                                                              
    library(haven);                                                                                                
    library(dplyr);                                                                                                
    library(tidyr);                                                                                                
    library(SASxport);                                                                                             
    have<-read_sas("d:/sd1/have.sas7bdat");                                                                        
    str(have);                                                                                                     
    want<-as.data.frame(have %>%                                                                                   
      group_by(NAME) %>%                                                                                           
      complete(DATE = seq.Date(min(DATE), max(DATE), by="month")));                                                
    write.xport(want,file="d:/xpt/want.xpt");                                                                      
    ');                                                                                                            
                                                                                                                   
    libname xpt xport "d:/xpt/want.xpt";                                                                           
    data want ;                                                                                                    
      set xpt.want;                                                                                                
      format date mmyys7.;  ;                                                                                      
      value=sum(0,value);                                                                                          
    run;quit;                                                                                                      
    libname xpt clear;                                                                                             
                                                                                                                   
                                                                                                                   
