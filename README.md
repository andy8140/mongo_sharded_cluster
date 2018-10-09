# mongo_sharded_cluster

#config shard replicat set
docker-compose exec shrs1 mongo --port 27018
rs.initiate()
var cfg = rs.conf()
cfg.members[0].host = 'shrs1:27018'
rs.reconfig(cfg)
rs.add('shrs1-2:27018')
rs.add('shrs1-3:27018')
rs.status()
quit()


docker-compose exec shrs2 mongo --port 27018
rs.initiate()
var cfg = rs.conf()
cfg.members[0].host = 'shrs2:27018'
rs.reconfig(cfg)
rs.add('shrs2-2:27018')
rs.add('shrs2-3:27018')
rs.status()
quit()


docker-compose exec shrs3 mongo --port 27018
rs.initiate()
var cfg = rs.conf()
cfg.members[0].host = 'shrs3:27018'
rs.reconfig(cfg)
rs.add('shrs3-2:27018')
rs.add('shrs3-3:27018')
rs.status()
quit()


sh.addShard('shrs1/shrs1:27018,shrs1-2:27018,shrs1-3:27018')
sh.addShard('shrs2/shrs2:27018,shrs2-2:27018,shrs2-3:27018')
sh.addShard('shrs3/shrs3:27018,shrs3-2:27018,shrs3-3:27018')
sh.status()
