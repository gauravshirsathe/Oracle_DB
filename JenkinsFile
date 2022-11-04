pipeline{
    agent any
    stages{
        stage("A"){
            steps{
                sh '''
                echo "Creating provider.tf file"
                sudo echo "provider \"oci\" {" >> /terraform/tf-provider/provider.tf
                sudo echo "tenancy_ocid = \"$TENANCY_OCID\"" >> /terraform/tf-provider/provider.tf
                sudo echo "user_ocid = \"$USER_OCID\"" >> /terraform/tf-provider/provider.tf
                sudo echo "private_key_path = \"$RSA_PRIVATE_KEY_PATH\" " >> /terraform/tf-provider/provider.tf
                sudo echo "fingerprint = \"$FINGERPRINT\"" >> /terraform/tf-provider/provider.tf
                sudo echo "region = \"$REGION_IDENTIFIER\"" >> /terraform/tf-provider/provider.tf
                sudo echo "}" >> /terraform/tf-provider/provider.tf

                echo "Creating availability-domains.tf file" >> /terraform/tf-provider/availability-domains.tf
                echo "# Source from https://registry.terraform.io/providers/hashicorp/oci/latest/docs/data-sources/identity_availability_domains" >> /terraform/tf-provider/availability-domains.tf
                echo "# <tenancy-ocid> is the compartment OCID for the root compartment." >> /terraform/tf-provider/availability-domains.tf
                echo "# Use <tenancy-ocid> for the compartment OCID." >> /terraform/tf-provider/availability-domains.tf
                echo "data \"oci_identity_availability_domains\" \"ads\" {" >> /terraform/tf-provider/availability-domains.tf
                echo " compartment_id = \"$TENANCY_OCID\"">> /terraform/tf-provider/availability-domains.tf
                echo "}" >> /terraform/tf-provider/availability-domains.tf

                echo "Creating outputs.tf file"
                echo "# Output the list of all availability domains. >>" >> /terraform/tf-provider/outputs.tf
                echo "output \"all-availability-domains-in-your-tenancy\" {" >> /terraform/tf-provider/outputs.tf
                echo "value = data.oci_identity_availability_domains.ads.availability_domains" >> /terraform/tf-provider/outputs.tf
                echo "}" >> /terraform/tf-provider/outputs.tf
                '''
            }
        }
    }
}
