# ICAPS-2018 Tutorial
Integrating Classical Planning and Mobile Service Robots using ROSPlan
----------------------------------------------------------------------
Oscar Lima and Rodrigo Ventura (DFKI, Germany, IST, Univ. Lisbon)

oscar.lima@dfki.de, rodrigo.ventura@isr.tecnico.ulisboa.pt

Tutorial website available [here](https://irsgroup.isr.tecnico.ulisboa.pt/tutorial-on-integrating-classical-planning-and-mobile-service-robots-using-rosplan/), tutorial slides available over there.

# INSTRUCTIONS FOR THE HANDS-ON SESSION

Step 1: Install virtual machine downloaded from here: https://goo.gl/C35Zym (in, e.g., VirtualBox, VMWare)

Step 2: Add the following line to the ~/.bashrc:

    source ~/ros_kinetic/ropslan/devel/setup.bash

Step 3: Clone the tutorial git repository containing example files from [SocRob@Home](https://irsgroup.isr.tecnico.ulisboa.pt/socrob/) team:

    cd ~/ros_kinetic/ropslan/src
    git clone https://github.com/oscar-lima/rosplan_tutorial.git
    cd rosplan_tutorial
    catkin build --this

Step 4: Fix PDDL domain:

    roscd rosplan_tutorial/common/pddl
    gedit domain.pddl

find and complete line:

    ; code find_object here !!!

Step 5: Fix PDDL problem instance:

    roscd rosplan_tutorial/common/pddl
    gedit problems/trivial.pddl
    locate line: ; fact missing here !!!
    add missing fact
  
Step 6: Check the PDDL domain and problem and test it:

    roscd rosplan_tutorial/common/pddl
    rosrun rosplan_planning_system popf domain.pddl problems/trivial.pddl

Step 7: Launch the ROSPlan system:

    roslaunch rosplan_tutorial gpsr_demo.launch

Step 8: Test the problem generator:

    rostopic echo /rosplan_problem_interface/problem_instance
    rosservice call /rosplan_problem_interface/problem_generation_server

Step 9: Test the planner interface:

    rostopic echo /rosplan_planner_interface/planner_output
    rosservice call /rosplan_planner_interface/planning_server

Step 10: Test the plan parser:

    rostopic echo /rosplan_parsing_interface/complete_plan
    rosservice call /rosplan_parsing_interface/parse_plan

Step 11: Test the plan dispatcher:

    rostopic echo /rosplan_plan_dispatcher/action_dispatch
    rostopic echo /rosplan_plan_dispatcher/action_feedback
    rosservice call /rosplan_plan_dispatcher/dispatch_plan
