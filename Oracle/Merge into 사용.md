
#### MySQL - ON DUPLICATE KEY
```mysql
insert into cms_main
			(
			siteid, maintype, rollyn, rolltime, insertdate, insertuser,
			insertip, modifydate, modifyuser, modifyip, delyn
			)
		values
			(
			#{siteid},#{maintype},#{rollyn},#{rolltime},
			#{insertdate},#{insertuser},#{insertip},
			#{modifydate},#{modifyuser},#{modifyip},#{delyn}
			)
		on duplicate key update
		rollyn=values(rollyn),
		rolltime=values(rolltime),
		modifydate=values(modifydate),
		modifyuser=values(modifyuser),
		modifyip=values(modifyip),
		delyn=values(delyn)
	</insert>
```

위의 코드는 기존에 INSERT문과 비슷하나 중간에 ON DUPLICATE KEY 문이 핵심이다.
만약 INSERT하려는 테이블에 VALUES값들이 이미 존재하고 있으면
ON DUPLICATE KEY를 이용하여 INSERT하지 않고, UPDATE 해준다.


#### Oracle - Merge into 사용
```oracle
<insert id="mainInsert">

		MERGE INTO cms_main
		USING DUAL
		ON (siteid = #{siteid} AND maintype = #{maintype} AND rollyn = #{rollyn} AND rolltime = #{rolltime}
			AND insertdate = #{insertdate} AND insertuser = #{insertuser} AND insertip = #{insertip} AND modifydate = #{modifydate}
			AND modifyuser = #{modifyuser} AND modifyip = #{modifyip} AND  delyn =#{delyn}
		)
		WHEN MATCHED THEN
		UPDATE SET
		rollyn= #{rollyn},
		rolltime= #{rolltime},
		modifydate= #{modifydate},
		modifyuser= #{modifyuser},
		modifyip= #{modifyip},
		delyn= #{delyn)
	</insert>
```

