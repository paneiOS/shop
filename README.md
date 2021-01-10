# shop
sping project

[DB 정보] 12.10 테이블 정보 수정 

[상품테이블] 
create table gds_info(
    gdsNum number primary key,
    gdsName varchar2(100) not null,
    cateCode number not null,
    gdsPrice number not null,
    gdsColor varchar2(100) not null, 
    gdsStock number null,
    gdsDetail varchar2(500) null,
    gdsImg varchar2(500) not null,
    thumbImg varchar2(100) not null,
    regDate date default sysdate,
    gdsDesc varchar2(100) null
);

create SEQUENCE gds_info_seq
INCREMENT by 1
start with 1;

insert into gds_info values(gds_info_seq.nextval,'Peony',1,2000,'pink,orange',20,'작약','1.jpg','1_thumb.jpg',sysdate,'1-description.jpg');
insert into gds_info values(gds_info_seq.nextval,'Rose',2,2500,'red,pink',50,'뉴던','2.jpg','2_thumb.jpg',sysdate,'2-description.jpg');
insert into gds_info values(gds_info_seq.nextval,'Sunflower',3,5000,'yellow',999,'맥시밀리언','3.jpg','3_thumb.jpg',sysdate,'3-description.jpg');
insert into gds_info values(gds_info_seq.nextval,'Plum blossom',4,3000,'red,orange',300,'동백꽃','4.jpg','4_thumb.jpg',sysdate,'1-description.jpg');
insert into gds_info values(gds_info_seq.nextval,'Cosmos',3,2800,'purple,white',300,'코스모스','5.jpg','5_thumb.jpg',sysdate,'3-description.jpg');
insert into gds_info values(gds_info_seq.nextval,'Tulips',1,2200,'orange,red,yello',100,'튤립','6.jpg','6_thumb.jpg',sysdate,'2-description.jpg');

[상품코드 테이블] 

create table cate_info(
  cateNum number primary key,
  cateName varchar2(100) not null,
  cateCode number not null
);

insert into cate_info values(1,'Spring',1);
insert into cate_info values(2,'Summer',2);
insert into cate_info values(3,'Fall',3);
insert into cate_info values(4,'Winter',4);


[리뷰테이블]

create table gds_review (
    rvNum      number       PRIMARY key,
    gdsNum      number          not null,
    id      varchar2(50)   not null,
    rvText      varchar2(2000)  not null,
    rvImg      varchar2(200)  null,
    rvDate     date            default sysdate,
    rvScore    number        not null
);

create sequence gds_review_seq
increment by 1
start with 1;

select * from gds_review;

insert into gds_review(rvNum, gdsNum, id, rvText, rvImg, rvDate, rvScore)
values(gds_review_seq.nextval,1,'id','test Text','test.jpg',sysdate,5);

[회원테이블]
create table user_info(
    userNum number primary key,
    name varchar2(20) not null,
    id varchar2(50) not null,
    pw varchar2(100) not null,
    email varchar2(50) not null,
    tel varchar2(20) not null,
    data Date, 
    mAddr varchar2(20) not null,
    lAddr varchar2(200) not null,
    dlAddr varchar2(100) not null,
    lastData date
);

create sequence user_num
    increment by 1
    start with 1
    minvalue 1
    maxvalue 1000
    nocycle;

select * from user_info;
insert into user_info(userNum, name, id, pw, email, tel, data, mAddr, lAddr, dlAddr)
VALUES(user_num.nextval,'name','id','pw','eamil','01033371996',sysdate,'1','1','1');

insert into user_info(userNum, name, id, pw, email, tel, data, mAddr, lAddr, dlAddr)
VALUES(user_num.nextval,#{name},#{id},#{pw},#{email},#{tel},sysdate,#{mAddr},#{lAddr},#{dlAddr});

[장바구니테이블] 

create table user_cart(
    cartNum number not null primary key,
    userNum number not null, 
    gdsNum  number not null, 
    cartCount number not null,
    cartColor varchar2(50) not null
);
create sequence cart_Num
    increment by 1
    start with 1
    minvalue 1
    maxvalue 1000
    nocycle;
 
[찜테이블]

create table user_like(
  likeNum number primary key,
  gdsNum number not null,
  userNum number not null
);

CREATE SEQUENCE user_like_seq
start with 1
INCREMENT by 1;

insert into user_like values(user_like_seq.nextval,1,6);

[쿠폰테이블]

drop table mgrCoupon purge;
create table mgrCoupon(
    mgrCp number primary key,
    cpName varchar2(50) not null,
    itemScope varchar2(50) not null,
    cpRate number not null,
    expDate varchar2(50) not null,
    cpCode varchar2(20) not null,
    cpCode2 varchar2(20) not null,
    cpCode3 varchar2(20) not null,
    cpCode4 varchar2(20) not null
);

drop sequence mgr_cp;
create sequence mgr_cp
    increment by 100
    start with 1111
    minvalue 1111
    maxvalue 5000
    nocycle;

insert into mgrCoupon(mgrCp, cpName, itemScope, cpRate, expDate, cpCode, cpCode2, cpCode3, cpCode4)
VALUES(mgr_cp.nextval,'VVIP','전체상품 적용가능',0.5,'2021.12.31','VVIP','VVIP','VVIP','VVIP');

insert into mgrCoupon(mgrCp, cpName, itemScope, cpRate, expDate, cpCode, cpCode2, cpCode3, cpCode4)
            VALUES(mgr_cp.nextval,'블랙프라이데이','전체상품 적용가능',0.3,'2020.12.31','AB12','AA11','BB22','12AB');

insert into mgrCoupon(mgrCp, cpName, itemScope, cpRate, expDate, cpCode, cpCode2, cpCode3, cpCode4)
VALUES(mgr_cp.nextval,'회원가입축하','전체상품 적용가능',0.15,'2021.01.01','CD23','CC22','DD33','23CD');

drop table coupon purge;
create table coupon(
    cpNum number primary key,
    cpCode varchar2(20) not null,
    userNum number not null,
    useCp varchar2(100) not null
);

drop sequence cp_num;
create sequence cp_num
    increment by 100
    start with 1111
    minvalue 1111
    maxvalue 5000
    nocycle;

[결제 테이블]

drop table payment purge;

create table payment(
  payNum number primary key not null,
  userNum  number not null,
  ordName      varchar2(500)   ,
  ordNum       varchar2(500)   ,
ordColor     varchar2(500)    , 
  ordCount     varchar2(500)        ,
  ordPrice     varchar2(500)        ,
 payDate          timestamp default systimestamp ,
 receiver      varchar2(100)    , 
 email       varchar2(100) ,
phone      varchar2(100) ,
addr1 varchar2(100) ,
    addr2 varchar2(200),
    addr3 varchar2(100)  ,
message varchar2(200),
depositor varchar2(100)  ,
bankName  varchar2(100),
payMethod varchar2(100),
cal number  ,
point number ,
usePoint number,
useCouponCal number,
cpNum number
);

drop sequence pay_num;
create sequence pay_num
    increment by 1
    start with 1
    minvalue 1
    maxvalue 1000
    nocycle;


[구매정보테이블] 
create table ordered_list(
  ordNum number PK not null,
  userNum number FK not null,
  gdsNum number FK not null,
  cpNum number FK not null,
  ordName varchar2(100) not null,
  shipFee number not null,
  ordCharge number not null,
  ordDate date not null,
  payMethod varchar2(100) not null,
  lastName varchar2(50) not null,
  lastTel varchar2(20) not null,
  lastDelivery varchar2(400)
);

