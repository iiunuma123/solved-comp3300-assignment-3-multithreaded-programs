Download Link: https://assignmentchef.com/product/solved-comp3300-assignment-3-multithreaded-programs
<br>
The aim of this assignment is to help students understand: (i) how to write multithreaded programs and consolidate the concepts learned in class; and (ii) the main concepts of multi-threaded programming with synchronization and thread scheduling. Students will obtain hands-on experience in working with POSIX PThreads (or, Windows Threads or Java Threads) and with OpenMP API (or, any implicit threading API of your choice). Use a thread API of your choice, though I prefer you use POSIX Pthreads API.

<strong>Tasks:</strong>

<ol>

 <li><u>Program-1</u>. An interesting way of calculating  is to use a technique known as <em>Monte Carlo</em>, which involves randomization. This technique works as follows. Suppose you have a circle inscribed within a square, as shown in the figure (assume that the radius of this circle is 1; thus we have a square of size 2×2).</li>

</ol>

First, generate s series of points as simple (<em>x, y</em>) coordinates. These points must fall within the Cartesian coordinates that bound the square. Of the total number of random points that are generated, some will occur within the circle. Next, estimate  by performing the following calculation:

 = 4  (<em>number of points in circle</em>) / (<em>total number of points</em>)

Write a multi-threaded version of this algorithm that creates a separate thread (the <em>slavethread</em>) to generate a number of random points. The slave-thread will count the number of points that occur within the circle (the hit_count) and store that result in the global variable circle_count. When the slave-thread has exited, the parent thread (the <em>master-thread</em>) will calculate and output the estimated value of . It is worth experimenting with the number of random points generated. As a general rules, the greater the number of random points, the closer the approximation of .

Below, are codes for generating random numbers, as well as codes for determining if the random (<em>x, y</em>) point occurs within the circle.

/* Generates a double precision random number */ double random_double()

{

return random() / ((double)RAND_MAX + 1);

}




/* seed the random number generator */       srandom((unsigned)time(NULL));




/*generate random numbers between -1.0 and +1.0 (exclusive)*/

/* to obtain a random (x, y) point*/  x = random_double() * 2.0 – 1.0;      y = random_double() * 2.0 – 1.0;




/* is (x, y) point within the circle ? */  if ( sqrt(x*x + y*y) &lt; 1.0 )

++hit_count; /* yes, (x, y) point is in circle */




<em>Note: Program-1 contains only 2 threads; a master-thread and its single slave-thread. </em>




<ol start="2">

 <li><u>Program-2</u>: Repeat Program-1 but instead of using a separate thread to generate random points, use OpenMP to parallelize the generation of points. Be careful not to place the calculation of  in the parallel region, since you want to calculate  only once.</li>

</ol>




<ol start="3">

 <li><u>Program-3</u>. Program-1 asked you to design a multi-threaded program that estimated  using the <em>Monte Carlo</em> In Program-1, you were asked to create a single slave-thread that generated random points, storing the results in a global variable circle_count. Once that slave-thread exited, the master-thread performed the calculation that estimated the value of . Modify Program-1 so that you create several slave-threads, each of which generates random points and determines if the points fall within the circle. Each slavethread will have to update the global count of all points that fall within the circle. Protect against race conditions on updates to the shared global variable by using mutex locks.</li>

</ol>




<em>Note: each slave-thread must generate </em><em>points_per_thread random points, which is the ratio of the total number of random points to the number of slave-threads. </em>




<ol start="4">

 <li><u>Program-4</u>. Program-2 asked you to design a program using OpenMP that estimated  using the <em>Monte Carlo</em> Examine your solution to Program-2 looking for any possible race conditions. If you identify a race condition, protect against it using the strategy outline in Section 5.10.2 of the textbook.</li>

</ol>




Let the constant NUMBER_OF_POINTS be the total number of random (<em>x, y</em>) points and the constant NUMBER_OF_SLAVES be the number of slave-threads.

<ol>

 <li>Run Program-1 and Program-2 with NUMBER_OF_POINTS = 100, 1000, 10000, 100000, 1000000, and return for each run both their execution times and their estimated  Write a short report in which you compare the running times and the estimated  values, and provide meaningful comments (one or two paragraphs) on your results. The comments should address the running times obtained and relate them to the concepts learned in class: (i) your multi-threaded Program-1 and Program-2 should run faster than a non-threaded program; (ii) Program-2 which uses OpenMP should run faster than Program-1; and (iii) a larger value of NUMBER_OF_POINTS should give a more accurate estimation of  than a smaller value.</li>

 <li>Run Program-3 and Program-4 with NUMBER_OF_POINTS = 1000000 and</li>

</ol>

NUMBER_OF_SLAVES = 2, 20, 40, 80, 100, and return for each run both their execution times and their estimated  values. Write a short report in which you compare the running times and the estimated  values, and provide meaningful comments (one or two paragraphs) on your results. The comments should address the running times obtained and relate them to the concepts learned in class: (i) your multi-threaded Program-3 and Program-4 should run faster than Program-1 and Program-2; (ii) Program-4 which uses

OpenMP should run faster than Program-3; (iii) a larger value of NUMBER_OF_SLAVES should give a faster running time than a smaller value; and (iv) what can you say about the estimated  values as NUMBER_OF_SLAVES changes from 2 to 100?


