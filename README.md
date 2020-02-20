# Wrapper around RobotPulse version >= 1.6.0

Latest version of thePulseApi: **pip3 install pulse-api -i https://pip.rozum.com/simple**

## Connect to robot:

                from newPulse import *
                host = '127.0.0.0:8081'
                robot = NewRobotPulse(host)

## New function:

*- set_reference_frame(robot_position)

Set reference frame in the respect to the robot base,
further robot works relative it.

                robot.set_reference_frame(position([x,y,z],[r,p,w]))
 
*- get_referance_frame()

Return a dict with keys 'point' and 'rotation'

                robot.get_reference_frame()

                >>> {'point': {'x': 0.0, 'y': 0.0, 'z': 0.0},
                     'rotation': {'roll': 0.0, 'pitch': 0.0, 'yaw': 0.0}}

*- run_positions(
            target_positions,
            speed=None,
            velocity=None,
            acceleration=None,
            tcp_max_velocity=None,
            motion_type=MT_JOINT
)

Starts the list of points recalculated relative to the reference coordinate system.


                target_positions = [
                    position([x, y, z], [r, p, w]),
                    position([x, y, z], [r, p, w])
                ]

                robot.run_positions(target_positions, speed=5)

*- set_position(
            target_position,
            speed=None,
            velocity=None,
            acceleration=None,
            tcp_max_velocity=None,
            motion_type=MT_JOINT
    )

Set the robot in the given position. If an reference frame is specified,
the robot moves relative to it.

                set_position(position([x, y, z], [r, p, w]), speed=5)

    - untwist()

        Allows the robot exit from TWISTED state, after the rotors were manually rotated into ~correct place

        '''html
        robot.untwist()

        >>> <Response [503]>  (if all is OK)
        '''

    - move_along_axis(axis, distance, velocity)

        Allows to move along one of each axis: 'x', 'y', 'z', 'roll', 'pitch', 'yaw'
        at a given distance, at a specified speed

        '''html
        axis = 'x'
        distance = 0.1
        velocity = 1

        robot.move_along_axis(axis, distance, velocity)
        '''
    - stop_by_digital_input(number_of_input)

        Stop the robot from the Digital Input

        '''html
        number_of_DI = 1
        robot.stop_by_digital_input(number_of_DI)
        '''

    - sensing(
        axis,
        detect_distance,
        velocity,
        retract_distance=0.01,
        retract_velocity=0.3,
        number_of_input=1
    )
        Mini case.

        '''html
        axis = 'x'
        detect_distance = 0.1
        velocity = 1
        robot.sensing(axis, detect_distance, velocity)
        '''

    - get_position_rel_base()

        Returns the position relative to the base, even if an reference frame is specified.

        '''html
        robot.get_position_rel_base()

        >>> {'point': {'x': -0.09161, 'y': -0.2911, 'z': 1.07063},
             'rotation': {'roll': 3.08421, 'pitch': 0.72008, 'yaw':0.17362}}
        '''

    - go_home(
        speed=None,
        velocity=None,
        acceleration=None,
        tcp_max_velocity=None,
        motion_type=MT_JOINT
    )
        Return the robot on home position pose[0, -90, 0, -90, -90, 0]

        '''html
            robot.go_home()
        '''

    - enable_moving_panel()

        Displays the robot control panel. Allows you to move the robot using buttons on the screen,
        displays the pose and position in the console.

        '''htm
        robot.enable_moving_panel()
        '''
