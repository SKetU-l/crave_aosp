## Building AOSP with foss.crave.io and its Devspace

**Are AOSP build times slowing you down?**

Crave.io can significantly accelerate your Android Open Source Project (AOSP) builds. This developer productivity platform reduces build times from hours to minutes, freeing you to focus on coding and innovation.

**Key Benefits:**

- **Faster Builds:** See your changes reflected in minutes, not hours.
- **Streamlined Workflow:** Build AOSP using your preferred IDE and tools.
- **Reduced Complexity:** No need to manage build dependencies or infrastructure.

**Getting Started with Crave.io:**

1. **Sign Up:** Join the crave.io [**Discord server**](https://discord.gg/EJxksGJEBS).
2. **Join Team AOSP:** Request access in the #ext-foss-aosp channel on Discord.
3. **Explore (Optional):** For an easier setup, check out [**crave_aosp_builder**](https://github.com/sounddrill31/crave_aosp_builder.git).
4. **Detailed Guide:** Visit the [**opendroid wiki**](https://opendroid.pugzarecute.com/wiki/Crave_Devspace) for a comprehensive guide.

**Accessing Devspace Locally:**

1. **Get Crave Configuration File:** Download your API key from the [**API Keys**](https://foss.crave.io/app/#/apikeys) tab.
2. **Setup Command Line Tool:** Download the crave binary from the [**Downloads**](https://foss.crave.io/app/#/downloads) tab and save it in your $PATH as "crave."

**Using Crave.io from a Cloud Server:**

1. **For Shell:** Use [**segfault shell**](https://shell.segfault.net/) in your browser. Save the provided SECRET.
2. **For SSH:**
   - Connect via SSH: `ssh root@segfault.net` (password: 'segfault').
   - Save the SSH line with the SECRET key.

3. **Setup Command Line Tool:**

   ```sh
   sudo apt-get update
   sudo bash -c "$(curl -fsSL https://github.com/accupara/crave/raw/master/get_crave.sh)"
   ```

**Joining Devspace:**

- Download or manually copy your crave.conf file from the [**API Keys**](https://foss.crave.io/app/#/apikeys) tab.
- Save the config manually by pasting the contents into a file on your server using `nano crave.conf`.
- Log into your devspace by running:

   ```sh
   crave -c ./crave.conf devspace
   ```

**Cloning a Project:**

1. **Enter Devspace:** Let's build LineageOS.
2. **Clone Project:** 
   ```sh
   crave clone list #to see all available projects
   crave clone create --projectID 72 lineageos

**Building the Project:**

1. **Start the Build:**

   ```sh
   crave run --no-patch -- "
   repo init -u https://github.com/LineageOS/android.git -b lineage-21.0 --git-lfs --depth=1 &&
   git clone https://github.com/username/local_manifest --depth 1 -b branch .repo/local_manifests &&
   /opt/crave/resync.sh &&
   source build/envsetup.sh &&
   lunch lineage_codename-ap1a-variant && make installclean && mka bacon"
   ```

2. **Check Logs:** Monitor your build logs on foss.crave.io.

**Syncing a Different ROM:**

1. **Sync and Build a Different ROM:**

   ```sh
   crave run --no-patch -- "
   repo init -u https://github.com/RisingTechOSS/android.git -b fourteen --git-lfs --depth=1 &&
   git clone https://github.com/username/local_manifest --depth 1 -b branch .repo/local_manifests &&
   /opt/crave/resync.sh &&
   source build/envsetup.sh &&
   lunch lineage_codename-ap1a-variant && make installclean && mka bacon"
   ```

2. **Important:** Only sync ROMs related to each other and avoid syncing different Android versions over the current one.

**Getting Build Outputs:**

1. **Retrieve Build Files:**

   ```sh
   crave pull out/target/product/codename/romname.zip
   ```

## Contribute

If you think this guide is missing something, feel free to submit a pull request or report an issue.
