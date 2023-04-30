Download Link: https://assignmentchef.com/product/solved-mobilerobotics-assignment-3-icp-non-linear-least-squares-optimization
<br>
<h2></h2>

<ul>

 <li>Please check Moodle for “TEAM-ID” and “TEAM-NAME” fields above. Some of your names have been edited because of redundancy/simplicity. Instructions for submitting the assignment through GitHub Classrooms/Moodle has been uploaded on Moodle. Any clarifications will be made there itself.</li>

 <li>Code must be written in Python in Jupyter Notebooks. You can use Assignment-1’s environment for this assignment. More instructions for setup provided as you progress through this assignment.</li>

 <li>Both the team members must submit the zip file.</li>

 <li>You are not allowed to use any external libraries (other than ones being imported below).</li>

 <li>Answer the descriptive questions in your own words with context &amp; clarity. Do not just copy-paste from some Wikipedia page. You will be evaluated accordingly.</li>

 <li>You could split the Jupyter Notebook cells where TODO is written, but please try to avoid splitting/changing the structure of other cells.</li>

</ul>

<h1>2          Question 1: Simple Non-Linear least squares for Gaussian function</h1>

First, go through the <a href="https://www.notion.so/saishubodh/From-linear-algebra-to-non-linear-weighted-least-squares-13cf17d318be4d45bb8577c4d3ea4a02#1de60a8465664d39a12af24353feef9e">solved example here</a> from the <a href="https://www.notion.so/saishubodh/Mobile-Robotics-2020-Students-Page-0b65a9c20edd4081978f4ffad917febb#a68cabac64754fa485144cc89b4b8c65">notes page</a>. After understanding this,

(1.1) Code it from scratch using numpy and try it out yourself for say different number of iterations with a certain tolerance for all 50 observations using Gradient Descent. Make the following plots using matplotlib: * Data and fit plot: Ground truth Gaussian, observations (points) &amp; predicted Gaussian on the same plot. * Cost function (∥<em>r</em>∥<sup>2</sup>) vs number of iterations

Experiment with the hyperparameters and compile your observations in a table. Clearly mention your hyperparameters with justification.

(1.2) You’ve used Gradient Descent above. Now implement Gauss-Newton and LM algorithms. To contrast between the three, you must experiment with * Different initial estimate: Can a particular algorithm handle if the initial estimate is too far from GT? * Different number of observations: Can a particular algorithm handle very less observations? * Add <a href="https://numpy.org/doc/stable/reference/random/generated/numpy.random.normal.html">noise</a> to your observations: Can a particular algorithm handle large noise? * What else can you think of? (For example, can an algorithm converge in less iterations compared to others?)

Make the plots (mentioned in 1.1) for all 3 algorithms. Report your observations in a table(s) (comparison between the three for different factors). You will be awarded depending on how comprehensive your experimentation is (which you have to explain below under “<strong>Answers for Question 1</strong>” section).

<h2>2.1         Code for Question 1</h2>

[ ]: <em># Only numpy &amp; matplotlib is sufficient for this question.</em>

<em>##############################################################################</em>

<em># TODO: Do tasks described in Question 1                             #</em>

<em>##############################################################################</em>

<em># Replace “pass” statement with your code (You can split this cell into</em>

<em># multiple cells if you wish to) </em><strong>pass</strong>

<em>##############################################################################</em>

<em>#                       END OF YOUR CODE                         #</em>

<em>##############################################################################</em>

[ ]: <em>## Define the plots inside a function above and call them in this cell one by</em>␣

<em>,</em><sub>→</sub><em>one. When I run this cell, all plots ## asked in Q1 should be generated.</em>

<em>##############################################################################</em>

<em># TODO: Plotting for Question 1   # </em><strong>pass</strong>

<em>##############################################################################</em>

<em>#                       END OF YOUR CODE                         #</em>

<em>##############################################################################</em>

<h2>2.2         Answers for Question 1</h2>

Add explanations for the answers along with tables here. ### Answer for 1.1 Explain your experimentations with justification here

<table width="271">

 <tbody>

  <tr>

   <td width="72">This</td>

   <td width="72">is</td>

   <td width="72">sample</td>

   <td width="56">table</td>

  </tr>

  <tr>

   <td width="72">sample 1</td>

   <td width="72">sample 1</td>

   <td width="72">sample 1</td>

   <td width="56">sample 1</td>

  </tr>

 </tbody>

</table>

<strong>2.2.1      Answer for 1.2</strong>

Explain your experimentations with justification here

<table width="271">

 <tbody>

  <tr>

   <td width="72">This</td>

   <td width="72">is</td>

   <td width="72">sample</td>

   <td width="56">table</td>

  </tr>

  <tr>

   <td width="72">sample 2</td>

   <td width="72">sample 2</td>

   <td width="72">sample 2</td>

   <td width="56">sample 2</td>

  </tr>

 </tbody>

</table>

<h1>3          Question 2: ICP Coding</h1>

Implement basic ICP algorithm with (given) known correspondences.

Let X be your point cloud observed from the initial position. Your robot moved and observed P1 as your current point cloud. Same with P2 under a different transformation. Now you wish to apply ICP to recover transformation between (X &amp; P1) and (X &amp; P2). Use <em>root mean squared error (rmse) </em>as the error metric.

[ ]: <em># HELPER FUNCTIONS: DON’T EDIT THIS BLOCK – If you want to test on more cases,</em>␣

<em>,</em><sub>→</sub><em>you can add code to this block but # DON’T delete existing code.</em>

<em># Visualizing ICP registration </em><strong>def </strong>plot_icp(X, P, P0, i, rmse):

plt.cla()

plt.scatter(X[0,:], X[1,:], c=’k’, marker=’o’, s=50, lw=0) plt.scatter(P[0,:], P[1,:], c=’r’, marker=’o’, s=50, lw=0) plt.scatter(P0[0,:], P0[1,:], c=’b’, marker=’o’, s=50, lw=0) plt.legend((‘X’, ‘P’, ‘P0′), loc=’lower left’) plt.plot(np.vstack((X[0,:], P[0,:])), np.vstack((X[1,:], P[1,:])) ,c=’k’)

plt.title(“Iteration: ” + str(i) + ” RMSE: ” + str(rmse))

plt.axis([-10, 15, -10, 15]) plt.gca().set_aspect(‘equal’, adjustable=’box’) plt.draw() plt.pause(2) <strong>return</strong>