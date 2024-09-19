version: '3'

services:
        dj-mariadb:
                image: mariadb
                volumes:
                        #「:」前面的部分是備份資料庫的路徑，可以避免重新部署後資料消失
                        - /home/baisp/backup:/var/lib/mysql
                environment:
                        - MYSQL_ROOT_PASSWORD=rootpw
                        - MYSQL_DATABASE=domjudge
                        - MYSQL_USER=domjudge
                        - MYSQL_PASSWORD=djpw
                ports:
                        - 13306:3306
                command:
                        --max-connections=1000
        
        dj-domserver:
                image: domjudge/domserver:latest
                volumes:
                        - /sys/fs/cgroup:/sys/fs/cgroup:ro
                environment:
                        - CONTAINER_TIMEZONE=Asia/Taipei
                        - MYSQL_HOST=mariadb
                        - MYSQL_ROOT_PASSWORD=rootpw
                        - MYSQL_DATABASE=domjudge
                        - MYSQL_USER=domjudge
                        - MYSQL_PASSWORD=djpw
                ports:
                        #「:」前面的port number是外部連進去的port，可以自由設置
                        - 80:80
                links:
                        - dj-mariadb:mariadb
        #judgehost可以依需要多設幾個，名字、hostname、DAEMON_ID記得改
        dj-judgehost_0:
                image: domjudge/judgehost:latest
                privileged: true
                hostname: judgedaemon-0
                volumes:
                        - /sys/fs/cgroup:/sys/fs/cgroup:ro
                environment:
                        - JUDGEDAEMON_PASSWORD=ISmfuM6JslmSG8xqpvqR5dmtLIMrDx5B
                        - CONTAINER_TIMEZONE=Asia/Taipei
                        - DAEMON_ID=0
                links:
                        - dj-domserver:domserver
        dj-judgehost_1:
                image: domjudge/judgehost:latest
                privileged: true
                hostname: judgedaemon-1
                volumes:
                        - /sys/fs/cgroup:/sys/fs/cgroup:ro
                environment:
                        - CONTAINER_TIMEZONE=Asia/Taipei
                        - DAEMON_ID=1
                        - JUDGEDAEMON_PASSWORD=ISmfuM6JslmSG8xqpvqR5dmtLIMrDx5B
                links:
                        - dj-domserver:domserver
        dj-judgehost_2:
                image: domjudge/judgehost:latest
                privileged: true
                hostname: judgedaemon-2
                volumes:
                        - /sys/fs/cgroup:/sys/fs/cgroup:ro
                environment:
                        - JUDGEDAEMON_PASSWORD=ISmfuM6JslmSG8xqpvqR5dmtLIMrDx5B
                        - CONTAINER_TIMEZONE=Asia/Taipei
                        - DAEMON_ID=2
                links:
                        - dj-domserver:domserver
        dj-judgehost_3:
                image: domjudge/judgehost:latest
                privileged: true
                hostname: judgedaemon-3
                volumes:
                        - /sys/fs/cgroup:/sys/fs/cgroup:ro
                environment:
                        - CONTAINER_TIMEZONE=Asia/Taipei
                        - DAEMON_ID=3
                        - JUDGEDAEMON_PASSWORD=ISmfuM6JslmSG8xqpvqR5dmtLIMrDx5B
                links:
                        - dj-domserver:domserver
        dj-judgehost_4:
                image: domjudge/judgehost:latest
                privileged: true
                hostname: judgedaemon-4
                volumes:
                        - /sys/fs/cgroup:/sys/fs/cgroup:ro
                environment:
                        - JUDGEDAEMON_PASSWORD=ISmfuM6JslmSG8xqpvqR5dmtLIMrDx5B
                        - CONTAINER_TIMEZONE=Asia/Taipei
                        - DAEMON_ID=4
                links:
                        - dj-domserver:domserver
        dj-judgehost_5:
                image: domjudge/judgehost:latest
                privileged: true
                hostname: judgedaemon-5
                volumes:
                        - /sys/fs/cgroup:/sys/fs/cgroup:ro
                environment:
                        - CONTAINER_TIMEZONE=Asia/Taipei
                        - DAEMON_ID=5
                        - JUDGEDAEMON_PASSWORD=ISmfuM6JslmSG8xqpvqR5dmtLIMrDx5B
                links:
                        - dj-domserver:domserver
