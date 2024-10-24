# mysql_wp_deployment
ana kaynak: https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/

yaml'larda pvc içlerine oluşturduğumuz storageclass'ı ekledik.
dokümanda service ayarı Loadbalancer idi, clusterIP olarak değiştirdik.
dokümandaki gibi kubectl apply -k ./ yaptık ve her şey oluştu.

openshift içine wordpress için route ekledik.

wordpress deployment apache hatası verdi. onun için de anyuid ayarı yaptık.
oc create sa nginx-sa
oc adm policy add-scc-to-user anyuid -z nginx-sa
oc set sa deploy wordpress nginx-sa
