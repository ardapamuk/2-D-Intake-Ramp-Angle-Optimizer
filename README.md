# 2-D-Intake-Ramp-Angle-Optimizer
2-D Intake Ramp Angle Optimizer with using 2-D Oblique Shock Relations

clc; clear ; close;
    gamma = 1.4; % Gas constant
 
    M0=3.2;  % Flight Mach Number
   syms x  

 a= 600 ; %Number of iteration for first Oblique Shock Optimizer
 highestvalue=0;  
 highest_c_x= 0 ;  
tic
      for i=1:1:a
         
          x = 20+ (i* 0.05) ;
          
         for j=1:1:700
         
          y = 20+ (j* 0.05) ;
           if y < 60 && y > x 
   
            
          for k=1:1:800  % number of iterattion for third oblique shock optimizer
              
          z= 20+ (k* 0.05) ;
      
        
             if z< 60 && z > y
            
          
                 
      
                 theta1=x; %first oblique shock angle
       theta2=y; %second oblique shock angle   
           
    
    theta3=z; %third oblique shock angle
   format long
     %1st shock
    delta1 = atand(2/tand(theta1)*(M0^2*sind(theta1)^2-1)/(M0^2*(gamma+cosd(2*theta1))+2));  % wedge angle 

    
    
Mn0 = M0*sind(theta1);
Mn1_1 = sqrt((1+(gamma-1)/2*Mn0^2)/(gamma*Mn0^2-(gamma-1)/2));
M1_1 = Mn1_1/sind(theta1-delta1); %Mach number after the oblique shock

Pt0 = (1+(gamma-1)/2*M0^2)^(gamma/(gamma-1));
P1_1 = ((2*gamma*M0^2*(sind(theta1))^2-(gamma-1))/(gamma+1));
Pt1_1 = P1_1*(1+(gamma-1)/2*M1_1^2)^(gamma/(gamma-1));
PR1 = Pt1_1/Pt0;

    %2nd shock

    delta2=  atand(2/tand(theta2)*(M1_1^2*sind(theta2)^2-1)/(M1_1^2*(gamma+cosd(2*theta2))+2));% wedge angle 

Mn2_2 = M1_1*sind(theta2);
Mn1_2 = sqrt((1+(gamma-1)/2*Mn2_2^2)/(gamma*Mn2_2^2-(gamma-1)/2));
    M1_2 = Mn1_2/sind(theta2-delta2); 
    
P1_2 = P1_1*((2*gamma*M1_1^2*(sind(theta2))^2-(gamma-1))/(gamma+1));
Pt1_2 = P1_2*(1+(gamma-1)/2*M1_2^2)^(gamma/(gamma-1)) ;
  PR2 = Pt1_2/Pt1_1; 
    %3rd shock 

    
    delta3= atand(2/tand(theta3)*(M1_2^2*sind(theta3)^2-1)/(M1_2^2*(gamma+cosd(2*theta3))+2)); % wedge angle 

   Mn3_3 = M1_2*sind(theta3); 
   
   Mn1_3 = sqrt((1+(gamma-1)/2*Mn3_3^2)/(gamma*Mn3_3^2-(gamma-1)/2));
   
   M1_3 = Mn1_3/sind(theta3-delta3);
   
   P1_3 = P1_2*((2*gamma*M1_2^2*(sind(theta3))^2-(gamma-1))/(gamma+1));
   
   Pt1_3 = P1_3*(1+(gamma-1)/2*M1_3^2)^(gamma/(gamma-1));
PR3 = Pt1_3/Pt1_2;
   
    %PR normal shock
    
    theta4 = 90 ; % for normal shock angle is 90 
   delta4 = atand(2/tand(theta4)*(M1_3^2*sind(theta4)^2-1)/(M1_3^2*(gamma+cosd(2*theta4))+2)); 
   
   Mn4_4 = M1_3*sind(theta4);
Mn1_4 = sqrt((1+(gamma-1)/2*Mn4_4^2)/(gamma*Mn4_4^2-(gamma-1)/2));
M1_4 = Mn1_4/sind(theta4-delta4); 

P1_4 = P1_3*((2*gamma*M1_3^2*(sind(theta4))^2-(gamma-1))/(gamma+1)); 

Pt1_4 = P1_4*(1+(gamma-1)/2*M1_4^2)^(gamma/(gamma-1));
PR4 = Pt1_4/Pt1_3;


    %Total Pressure Recovery 

    TPR= PR3*PR2*PR1*PR4 ;


   
  
          
         if  TPR  >  highestvalue
             highestvalue= TPR ;    
             highest_c_x= x ;
              highest_c_y= y ;
               highest_c_z= z ;
         end  
         
             end
     
                end
             end
         end
          
             end
          toc

        
  highestvalue= TPR     % Highest Total Pressure Recovery found 
  highest_c_x= x        % First Oblique Shock Angle   
  highest_c_y= y        % Second Oblique Shock Angle
  highest_c_z= z        % Third Oblique Shock Angle
