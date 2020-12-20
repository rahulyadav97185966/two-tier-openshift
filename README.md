# two-tier-openshift

    oc new-app --name mysysql1 --docker-image=registry.lab.example.com/rhscl/mysql-57-rhel7 --env MYSQL_ROOT_PASSWORD=cetterede --env MYSQL_DATABASE=mydata --env                           MYSQL_USER=user1 --env MYSQL_PASSWORD=redhat  :- --docker-image is the internal registry image is used you can user only mysql:5.6 instide if that. --env is environment variable which a mandatory for mysql login.
    104  oc get pods -w :- you can able to see you pods deployment.
    105  oc get pods
    106  oc exec -it mysysql1-1-n8jv8 bash
    107  vi pv.yml  :- we have to attach pv and pvc for this so we are going to create a pv for it.
    108  oc create -f pv.yml 
    109  oc get pv
    110  vi pvc.yml 
    111  oc create -f pvc.yml 
    112  oc get pv,pvc
    113  oc get dc
    114  oc edit dc mysysql1  :- here we have to edit persistent volume claim name :- 
              - name: mysql-volume-1
                persistentVolumeClaim:
                  claimName: myclaim
    115  oc get pods -w
    116  oc get pods
    117  vi pv.yml 
    118  oc create -f pv.yml 
    119  oc get pv
    120  vi pvc.yml 
    121  oc create -f pvc.yml 
    122  oc get pv,pvc
    123  wget http://classroom.example.com/content/wordpress.tar :- fetched file.
    124  ls
    125  docker load -i wordpress.tar 
    126  docker images
    127  docker tag docker.io/wordpress registry.lab.example.com/openshift/wordpress
    128  docker images
    129  docker push registry.lab.example.com/openshift/wordpress
    131  oc new-app --name wordpress --docker-image=registry.lab.example.com/openshift/wordpress --env DB_HOST=mysql --env DB_PASSWORD=cetterede
    132  oc get pods -w
    133  oc logs -f wordpress-1-g92bw 
    134  oc set volumes --help
    135  oc get pv,pvc
    136  history 
    137  oc get pods 
    138  oc create sa mysa  :- deu to privileged port we need to bind them, hence we have to create a service account for this.
    139  oc adm policy add-scc-to-user anyuid -z mysa :- adding policy to the servife account.
    140  oc get dc
    141  oc edit dc wordpress 
    142  oc get pods -w
    143  oc get posds
    144  oc get pods
    145  oc get svc
    146  oc get dc
    147  oc edit dc wordpress 
    148  oc get pods -w
    149  oc get pods
    150  oc get svc
    151  oc expose svc wordpress 
    152  oc get route
    153  oc get pods
    155  oc get svc
