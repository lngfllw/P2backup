#include "ros/ros.h"
#include "geometry_msgs/Twist.h"
//TODO: include ball_chaser DriveToTarget header file
#include "ball_chaser/DriveToTarget.h"

//ROS::Publisher motor commands;
ros::Publisher motor_command_publisher;

//TODO: create handle_drive_request callback fn that executes whenever a drive_bot service is requested
//this fn should publish requested linear x and angular velocities to the wheel joints
//after publishing requested velocities, message feedback should be returned with reuested wheel velocities

bool handle_drive_request(ball_chaser::DriveToTarget::Request& req, ball_chaser::DriveToTarget::Response& res)
{
//    ROS_INFO("DriveToTargetRequest received", (float)req.linear_x, (float)req.angular_z );

        //create motor_command object of type geometry_msgs::Twist
        geometry_msgs::Twist motor_command;
        //get commands from request
        motor_command.linear.x = req.linear_x;
        motor_command.angular.z = req.angular_z; 
        //publish angles to drive the robot
        motor_command_publisher.publish(motor_command);

        //return response message
        res.msg_feedback = "motor_command: lin_x = " + std::to_string(req.linear_x) + " ; ang_z = " + std::to_string(req.angular_z);

        ROS_INFO_STREAM(res.msg_feedback);

        return true;

}

int main(int argc, char** argv)
{
    //initialize ros node
    ros::init(argc, argv, "drive_bot");

    //create ros nodehanlde object
    ros::NodeHandle n;

    //inform ros master that we publish msg of type geometyr_msgs::Twist on robot actuation topic with publishing que size of 10
    motor_command_publisher = n.advertise<geometry_msgs::Twist>("/cmd_vel", 10);

    //TODO: define a drive /ball_chaser/command_robot service with handle_drive_request callback fn
    ros::ServiceServer service = n.advertiseService("/ball_chaser/command_robot", handle_drive_request);

    //TODO: delete the loop, move the code inside of the callback fn, make necessary changes to publish requested velocities instead of constant values

//    while (ros::ok()) {
//        //create motor_command object of type geometry_msgs::Twist
//        geometry_msgs::Twist motor_command;
//        //set wheel velocities forward [0.5, 0.0]
//        motor_command.linear.x = 0.5;
//        motor_command.angular.z = 0.0; 
//        //publish angles to drive the robot
//        motor_command_publisher.publish(motor_command);
//    }

    //TODO: handle ros communication events
    ros::spin();

    return 0;
}
