# mysql_wp_deployment
ana kaynak: https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/

burada openshift üzerine kendi oluşturduğumuz scdeneme isimli storageclass kullanarak mysql-wordpress deployment yapmayı amaçladık.
her durumda ana kaynak dokümanı mutlaka incelenmeli.

yaml'larda pvc içlerine oluşturduğumuz storageclass'ı ekledik.
dokümanda service ayarı Loadbalancer idi, clusterIP olarak değiştirdik.
dokümandaki gibi kubectl apply -k ./ yaptık ve her şey oluştu.

openshift içine wordpress için route ekledik.

wordpress deployment apache hatası verdi. onun için de anyuid ayarı yaptık.
oc create sa nginx-sa
oc adm policy add-scc-to-user anyuid -z nginx-sa
oc set sa deploy wordpress nginx-sa
