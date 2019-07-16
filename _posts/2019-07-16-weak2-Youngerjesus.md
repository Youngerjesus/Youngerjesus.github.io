---
layout: post
title:  "Week 2 capstone Identity "
date:   2019-07-09 11:36:36 +0530
tags: [identity, blockchain, Identity Management,uPort]
author: Youngerjesus
categories: blockchain uPort capstone 
---

<pre style="white-space: pre;
    word-break: break-word;">
<img src="{{ "/assets/img/measure.png" | relative_url }}" alt="">

<code> the following major requirements </code> 
    Security, Low cost, Portable 
    
<code> BlockID + uPort </code>
    정부 발급 ID로부터 디지털 ID를 구성하여 블록체인 기반 트랜잭션 시스템에 대한 음주 측정을 올바르게 수행하는 데 도움이 된다.
    the Identity creattion component는 사용자가 사용할 수 있는 디지털 ID 생성할 수 있고 the Identity Management 컴포넌트는 발급된 디지털 ID의 사용을 감시할 책임이 있다.

    Smart Contractss allow user to decide what keys have control over their identity. Furthermore uPort provides a 
    simple and clear way for users to interact wiith the Klaytn blockchain 

    Participants and Security Assumptions
        User
            A user is a person who participates the operation of the a transaction
            The user needs to obtain a digital identity from the identity creator, be used on the blockchain to identify him/herself
        Smartphone
            A smartphone belongs to a user, and is used by the user as his/her identity to interact with the blockchain based system
            (스마트 컨트랙트)
        Identity creator - Identity Manager 
            Identity creator is a centralized party that helps the user to create a digital identity that can be used in the blockchain system.    
        음주 측정기 
            the score is above the pre-configured threshold, the processor will generate the signature which will be passed via a direct register write, and sent to the blockchain. 

<code> 어떻게 Digital ID Creation을 만드는가 </code>
    To create a digital ID that is used in the blockchain-based system, 
    The user needs to bring his/her government issued ID and a smart-phone with biometric authentication mechanism to the identity creator
    
    
    Protocol 1 Digital ID creation. - (이 부분을 그림과 같이해서 )
    Require: The user u with government ID(id) and smart-phone(ph), the identity creator(c).

    u sends id to c;  -  버스 기업의 회원임을 나타내는 증거(신분증, 사진)
    
    c checks  -   
        • cdt1: the validity of id() ;
        • cdt2: consistency of id() and u; if cdt1 = cdt2 = true then  

    u provides ph to c;
    if u can unlock ph using biometric information then
        c and ph together run (pk,sk) ←KeyGen; - 키페어 생성 
        sk is securely stored in ph;
        c collects information i about u from id ;
        c generates a new proxy cert including both pk and i, and authenticate cert with its private key; return cert;
        -   여기서 키 쌍만을 만들고 그 사람만을 위한 digital identify를 생성시켜주기 위해서 new Proxy를 만들어준다 (정확하게 여기서 digital identify는 new Proxy의 address이다 ) 
            그리고 그 new Proxy에 공개키를 등록해주고 오로지 그 사람만이 이 proxy에 연결하는게 가능하고 한 proxy에 한개의 device만을 연결하도록한다.     
    end if 
    end if
    return fail

    If Protocol 1 succeeds, u’s digital identity that can be used in the blockchains system for other users to recognize u. 

<code> Contract  (controller -> proxy -> register ) </code>
    an instantiation of the controller with a link to the just created public key is made. 
    After that a new proxy is created with a link to that controller instance 
    and only that controller instance is able to invoke the proxy’s functions.
    The uPort identifier (uPortID) is now the address of the newly created proxy
    
    The RecoverableController is the contract that controls access to a Proxy.
        It allows a key, which exists only on a user's phone, to use the Proxy contract it has control over
        The RecoverableController, as its name hints, also gives users the ability to recover their Proxy if they lose their phone (and thus their key). 
        Users do so by declaring some recoveryKey — a key with the power to give a user control of their Proxy agai)
        To store identity attributes a global smart contract called registry is used.)    
        
    Proxy가 뭔데? 
        The Proxy contract is the most basic building block of a uPort identity. 
        A new Proxy is deployed for each new identity, and its address is the identifier of that identity. 
        This means that controlling access to the Proxy is controlling access to the identity.
        The Proxy contract does exactly what it sounds like: it allows a certain address to interact with the blockchain through itself. 
        Effectively, it is the avenue through which users interact with the rest of the Ethereum world. 
        This allows a user to continue interacting with other smart contracts from a single address, even in the case of key loss.



<code> Major operations of digital ID management include adding a new digital identity and disabling an existing identity. </code>
        we denote the group of nodes that are responsible for digital ID management as Gm)
        1. Adding a new digital identity
            After cert is created, it is submitted to the blockchain system, and nodes in Gm run a consensus protocol to determine whether it should be accepted in the blockchain or not

        2. Disabling an existing identity
            In case a user loses his/her private key sk that is stored in the smart-phone, he/she can submit a request transaction to the blockchain to ask to revoke correspon- ding cert
        
        3. Recovering a digital Identity
            Because the private key is only stored on the user’s mobile phone which can get lost, 
            uPort has a system that enables its users to regain control of their identity with a different key)

            기존의 과정             
            The user nominates a group of trustees (with their uPortID) in advance. 
            The trustees can then vote to change the associated public key of the user’s uPortID with a new one 
            and the key will be changed once a quorum is reached.)

            the Identity Management를 이용한 과정 
                The RecoveryQuorum contract allows a user to create a list of “delegates” that act as the recoveryKey mentioned above. 
                Essentially, these delegates can vote to restore a user’s Proxy to its rightful owner in the case of key loss.
                The delegates must have a uPort identity, as they are given voting power in the RecoveryQuorum through their own Proxy contracts.


    
<code> Protocol 2 Use of digital ID - proxy에서 a global register contract를 이용해서 블록체인 상에 음주 측정 기록을 저장하는 것 </code>
    Require: The user u with smart phone(ph), the blockchain system bc.
        u want to submit a transaction tr to blockchain; 
        u unlock ph using his/her biometric information
        if ph accepts u’s biometric then
            음주 측정을 한 후 
            ph uses sk to generate a digital signature sig of tr and returns it to u;
            u submits siд to bc;
            return succeed; 
        end if
    end if
    return fail
    - 여기서 개인키 sk와 음주 측정기는 스마트폰 하드웨어에 의해 보호된다 구체적으로는 TrustZone 기술을 사용한다. (Confidentiality/integrity 
    - TrustZone은 외부로 전송하지 못하게 하고 오로지 허용가능한 소프트웨어만 사용가능하게 한다

    -  when a user receives a transaction from blockchain, 
    -  the smart-phone will throw a FIQ (Fast Interrupt) exception to enter the secure mode 
    -  This mode turns our blockchain application in an isolated state that will not be affected by any malware infection.
    -  Once the FIQ exception is thrown, APB (AXI to Advanced Peripheral Bus Bridge) will then request the I/O Controller enable the fingerprint sensor. 
    -  The application will now request the user to submit a fingerprint for verification.                                                    
    -  Once the fingerprint has been processed and if the score returned by the controller is below a set threshold, the verification will fail
    -  음주 측정을 한 후 the score is above the pre-configured threshold, the processor will generate the signature which will be passed via a direct register write, and sent to the blockchain. 
        Then the blockchain can verify and complete the transaction.
    
    the user needs to unlock the smart-phone by using the his/her biometric information. Once this is done, at this moment, 
    government ID and the smart-phone link to a same person. The identity creator then generates a public and a secret key.
    The secret key will be stored in the TrustZone of a smart-phone for future authentication 
    Meanwhile, the identity creator will also generate a certificate including public key and all user information which is read from the ID card.
    This certificate can be used for other blockchain nodes to verify the user. 
    The use of digital ID is simple and quick. Just like other biometric ID scenarios (i.e. Android Pay), 
    if the user recognizes the transaction from blockchain, 
    he/she uses their biometric information to unlock the smart-phone. 
    In this case, the smart-phone switches to secure mode. 
    Then the smart-phone can retrieve the secret key from TrustZone and sign the transaction by the secret key. 
    Other blockchain nodes can verify the signature easily because a certificate with a public key can be found in the blockchain.



<code>TrustZone</code>
    The proposed system can be used in any smart phone with a processor that works with fingerprint biometric sensor. In order to be “finger-print-enabled”, 
    the processor must be an ARMv6KZ or later architecture
    The reason is that previous ARM architecture does not have TrustZone implemented. 
    TrustZone is a secure memory enclave which is developed to protect fingerprint data
    It is almost impossible for someone to reverse engineer the actual fingerprint image from this enclave.
    Confidentiality and integrity of the secret sk is protected by the hardware of the smart-phone. 
    Specifically, TrustZone technology is used and sk is stored in the “secure world”. 
    The hardware only allows authorized software to use the secret to generate signatures but never transfers it to the outside world.



<code> Biometric Authentication Mechanism on Smart-Phones </code>
    각종 스마트폰에 인증이 적용되려면 생체인증 하드웨어를 각 기기에 설치해야 한다.
    (In order for authentication to be applicable to various smart-phones, biometric authentication hardware needs to be installed on each device)
        
        Retina scanning(fingerprint 말고도 생체인식은 여러개가 잇다)
            Retina scanning has a low occur- rence of false positives and high processing speed based on Roberts’ research [12]. However, it also involves some disadvantages, e.g. low accuracy under an eye disease and high equipment cost. 
        
        Voice recognition
            simply compare the user’s voice with the archived record from the phone owner. By adopting toolkit like openSMILE[4], 
            smart-phone can quickly extract features from voice and verify whether the voice matches the trained model.
        
        Face recognition 
            is a technology which has been evolving since it was invented. 
            Typically, smart-phone uses the front camera and takes flat pictures of user’s face. 
            In this way, the system can be easily intruded with a similarly flat photo from the phone owner. 
            A more secure and accurate way is to utilize depth-camara to reconstruct a 3D model of a face.
    
        Touch fingerprint sensing module.
            The three parties are the User, Smart-phone and Blockchain. The User wants to authorize a transaction from Blockchain using a Smart-phone.
            Then the User submits their fingerprints to the Smart-phone, which would be checked with the stored fingerprint later. 
            The stored fingerprint is protected by TrustZone.

        Verifying a user.
            The most common way is face recognition because usually an ID card contains a face photo of its owner.
            During identification, the identity creator will take a picture of the object to be verified, 
            and send to the govern- ment database via a secure channel. 
            If a matched result is found in the database by artificial intelligence technology, the verification process succeeds


    
References 
    http://blog.daum.net/_blog/BlogTypeView.do?blogid=0Idbt&articleno=7593753&categoryId=404972&regdt=20151005145502
    https://medium.com/uport/making-the-uport-smart-contracts-smarter-e1798d8c1cf9
    https://github.com/uport-project/specs/#identities
    https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2DjfY
    https://medium.com/uport/making-uport-smart-contracts-smarter-part-2-introducing-identitymanager-af656ba7441b

</pre>