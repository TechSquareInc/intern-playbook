# 💾 Using Veracrypt

*Veracrypt is a free and open-source disk encryption software that allows users to encrypt entire storage devices or create encrypted containers to protect senstive data.*

---

## Installing Veracrypt

1. Download the current version of Veracrypt from the [Veracrypt website](https://www.veracrypt.fr/en/Downloads.html). 

2. Verify the files were downloaded, then use **tar -xvf veracrypt-1.** ***Current_Version_Number*** **-setup.tar.bz2**

3. Run the set up you wish to use. [Click here for a GUI tutorial](https://www.veracrypt.fr/en/Beginner%27s%20Tutorial.html).

![](https://user-images.githubusercontent.com/39737662/42830305-0e5ff538-89b9-11e8-9c9f-97bf171c0d6d.png)


4. Follow the brief set up process for Veracrypt.

![](https://user-images.githubusercontent.com/39737662/42830306-0e70cb10-89b9-11e8-8a90-95e2c6d04a99.png)

5. Scroll to the bottom of the terms and conditions or jump to the end by pressing q.

![](https://user-images.githubusercontent.com/39737662/42830307-0e803550-89b9-11e8-85a5-d82e7476be7f.png)

6. Now that Veracrypt is installed, it can be run anywhere to create encrypted file containers. To begin, use the touch command to create a file that will be converted to an encrypted file container. For example, bar.txt will become an encrypted file container, located on the path /home/cmerrick/foo/bar.txt

7. To begin, use **veracrypt -c** . It will ask several questions about what type of container you want to use, what form of encryption, what file system to use. Make sure to put the entire path to the container you wish to create. It will then prompt you to enter a passphrase twice, the longer the passphrase the more secure the container.

![](https://user-images.githubusercontent.com/39737662/42830308-0e97b9b4-89b9-11e8-9b14-41e5bef39e9c.png)

![](https://user-images.githubusercontent.com/39737662/42830309-0ea38d70-89b9-11e8-9a8a-b95acf0f7931.png)

![](https://user-images.githubusercontent.com/39737662/42830310-0eb58f34-89b9-11e8-9a10-8f1828143b14.png)

8. After creating the container, in order to access it, you must first mount it. To do this use **veracrypt /path/to/container /path/to/mount/point**. You can mount the container anywhere, it does not need to be at the original location it was made at. To unmount containers simply use **veracrypt -d**

> **Note:** Containers will automatically unmount at shutdown but will remain mounted if the user only logs off.

![](https://user-images.githubusercontent.com/39737662/42830313-1135263e-89b9-11e8-840b-8848529ee42c.png)

![](https://user-images.githubusercontent.com/39737662/42830314-114a0298-89b9-11e8-9fb2-36b60d11ed1e.png)

9. For any questions, consult **veracrypt --help** 

![](https://user-images.githubusercontent.com/39737662/42830315-115ec75a-89b9-11e8-88aa-8933c1cd6fd6.png)

## Resources

- [Veracrypt Documentation](https://www.veracrypt.fr/en/Documentation.html): The official documentation page for Vercrypt.
- [Beginner's Tutorial](https://veracrypt.io/en/Beginner's%20Tutorial.html): Step-by-step instructions on how to create, mount, and use a VeraCrypt volume.
